# Git Project Upload Operation Notes

## 1. Initialize Git Repository and Make the First Commit

```bash
cd ~/Documents/sim_snakemake_1

git init
git add .
git commit -m "Initial commit"
```

## 2. Create a New Repository on GitHub

- Create a new repository via the webpage: https://github.com/new
- **Do not** check README, LICENSE, or .gitignore.
- Example repository URL: https://github.com/cecilia9898/dictys_snakemake.git

## 3. Add Remote and Push

```bash
git remote add origin https://github.com/cecilia9898/dictys_snakemake.git
git branch -M main
git push -u origin main
```

## 4. Delete Unnecessary Files on GitHub

```bash
git pull origin main
git rm a.txt 1.ipynb EOF
git commit -m "Remove unnecessary files"
git push
```

## 5. Add a README.md File

```bash
nano README.md
# Paste project description, then save and exit

git add README.md
git commit -m "Add project README"
git push
```

## 6. Optional: Add a .gitignore File

```bash
echo "*.ipynb" >> .gitignore
echo "*.log" >> .gitignore
echo "log/" >> .gitignore

git add .gitignore
git commit -m "Add .gitignore"
git push
```

## 7. GitHub Repository URL

```
https://github.com/cecilia9898/dictys_snakemake
```

## 8. Add a Second Remote, e.g., backup

```bash
git remote add backup https://github.com/your_username/your_repository.git
```

- Push to the first remote (origin)
```bash
git push origin main
```

- Push to the second remote (backup)
```bash
git push backup main
```

- Configure Git to push to multiple remotes at once
```bash
git remote set-url --add --push origin https://github.com/your_old_repo.git
git remote set-url --add --push origin https://github.com/your_username/new_repo.git
```

## 9. Create a toc.md File to Record Workflow Steps

```bash
cat > toc.md << EOF
```

## 10. Update GitHub Repository Code

```bash
git status
cd ~/Documents/sim_snakemake_1
git add .
git commit -m "Update workflow"
git push origin main
git push backup main
```

## 11. Record GitHub Repository and Associated Naming

- `origin main` → cecilia9898/dictys_snakemake
- `backup main` → grnlab/private_netlib_pipeline
- `sfcm main` → grnlab/private_netlib

## 12. Cancel a git init Request

```bash
cd "/Users/zixuanye/Desktop/3 - Yu Lab"
rm -rf .git
```

---

