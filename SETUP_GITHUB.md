# Setting Up GitHub Repository

## Steps to Create and Push

1. **Create the repository on GitHub:**
   - Go to: https://github.com/organizations/conceptual-machines/repositories/new
   - Repository name: `magda-dsl`
   - Description: "MAGDA DSL - Domain Specific Language for DAW control"
   - Visibility: **Public** (open source)
   - **DO NOT** initialize with README, .gitignore, or license (we already have these)

2. **Add remote and push:**
   ```bash
   cd /Users/lucaromagnoli/Dropbox/Code/Projects/magda-dsl
   git remote add origin https://github.com/conceptual-machines/magda-dsl.git
   git branch -M main
   git push -u origin main
   ```

3. **Verify:**
   - Check https://github.com/conceptual-machines/magda-dsl
   - Ensure all files are present
   - Verify LICENSE is recognized by GitHub

## Repository Settings

After creating, configure:

1. **Settings → General:**
   - Add topics: `magda`, `daw`, `dsl`, `music-production`, `parser`
   - Add description: "Domain Specific Language for MAGDA - functional scripting for DAW control"

2. **Settings → Branches:**
   - Set default branch to `main`
   - Add branch protection rules (optional, for later)

3. **Settings → Pages:**
   - Enable GitHub Pages if you want documentation site (optional)

4. **Settings → Actions:**
   - Enable Actions for CI/CD (optional, for later)

## Next Steps After Push

1. Create first release: `v0.1.0`
2. Add GitHub Actions for testing (optional)
3. Set up issue templates (optional)
4. Add CODEOWNERS file (optional)

