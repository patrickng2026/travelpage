# /gitpush

Push the current project to GitHub safely with a README, GitHub Pages workflow, and updated repo description.

## Steps to follow (in order):

### Step 1 — Security scan
Scan every file in the project for secrets before touching git. Search for patterns including:
- API keys (patterns like `sk-`, `ghp_`, `AIza`, `Bearer `, `api_key`, `apikey`, `API_KEY`)
- Passwords or secrets in config files
- `.env` files containing real values
- Hardcoded tokens or credentials

If any real secrets are found, STOP and tell the user exactly which file and line contains the secret, and ask them to remove it before continuing. Do NOT push if secrets are detected.

If a file only contains a placeholder like `"YOUR_API_KEY_HERE"` that is safe — do not flag it.

Ensure a `.gitignore` exists that excludes:
```
.env
*.env
.env.local
*.pem
*.key
secrets/
node_modules/
.claude/settings.local.json
```

### Step 2 — Generate README.md
Read the project files and generate a professional `README.md` that includes:
- Project name and one-line description
- Screenshot or demo link (use the GitHub Pages URL if known)
- Features list (summarised from the actual code)
- How to run locally (just "open index.html in a browser" for static sites)
- Tech stack used
- Live demo link if GitHub Pages is configured

Write the README.md to the project root. Do not add a "Contributing" or "License" section unless the project already has one.

### Step 3 — Ensure GitHub Pages workflow exists
Check if `.github/workflows/deploy.yml` exists. If it does not, create it:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v5
      - uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
      - uses: actions/deploy-pages@v4
        id: deployment
```

### Step 4 — Push to GitHub
Run the following using PowerShell. Always prepend `$env:PATH += ";C:\Program Files\Git\cmd"` to ensure git is found.

```powershell
$env:PATH += ";C:\Program Files\Git\cmd"
cd "<project directory>"
git add .
git commit -m "<auto-generate a short, meaningful commit message based on recent changes>"
git push origin main
```

If the repo has not been initialised yet, run `git init`, `git branch -M main`, and `git remote add origin <url>` first.

If the push is rejected due to diverged history, use `git push origin main --force` since this is the user's own project.

### Step 5 — Enable GitHub Pages and update repo description
Use the GitHub token stored in Windows Credential Manager to call the GitHub API. Use this PowerShell pattern to retrieve it:

```powershell
Add-Type -TypeDefinition @'
using System;
using System.Runtime.InteropServices;
public class CredVaultCmd {
    [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Unicode)]
    public struct CREDENTIAL {
        public int Flags; public int Type; public string TargetName;
        public string Comment; public System.Runtime.InteropServices.ComTypes.FILETIME LastWritten;
        public int CredentialBlobSize; public IntPtr CredentialBlob;
        public int Persist; public int AttributeCount; public IntPtr Attributes;
        public string TargetAlias; public string UserName;
    }
    [DllImport("advapi32.dll", CharSet=CharSet.Unicode, SetLastError=true)]
    public static extern bool CredRead(string target, uint type, uint flags, out IntPtr credential);
    [DllImport("advapi32.dll")] public static extern void CredFree(IntPtr buffer);
    public static string GetPassword(string target) {
        IntPtr ptr; if (!CredRead(target, 1, 0, out ptr)) return null;
        var c = Marshal.PtrToStructure<CREDENTIAL>(ptr);
        var pass = Marshal.PtrToStringUni(c.CredentialBlob, c.CredentialBlobSize/2);
        CredFree(ptr); return pass;
    }
    public static string GetUser(string target) {
        IntPtr ptr; if (!CredRead(target, 1, 0, out ptr)) return null;
        var c = Marshal.PtrToStructure<CREDENTIAL>(ptr);
        CredFree(ptr); return c.UserName;
    }
}
'@
$token = [CredVaultCmd]::GetPassword("git:https://github.com")
$user  = [CredVaultCmd]::GetUser("git:https://github.com")
```

Then use `$token` to:

**Enable GitHub Pages** (if not already enabled):
```
POST https://api.github.com/repos/{owner}/{repo}/pages
Body: {"source":{"branch":"main","path":"/"}}
```

**Update repo description and website:**
```
PATCH https://api.github.com/repos/{owner}/{repo}
Body: {"description":"<one-line project description>","homepage":"https://{owner}.github.io/{repo}"}
```

If Pages is already enabled, skip the POST and only do the PATCH.

### Step 6 — Report back
Tell the user:
- ✅ Which files were pushed
- ✅ The live GitHub Pages URL
- ✅ The GitHub repo URL
- ✅ Confirmation that no secrets were uploaded
