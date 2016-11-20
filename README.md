```bash
# 01. create repo (repo A)
mkdir A
cd A
git init
# 02. repo A: create 1st commit with some files (file A, file B)
touch A
touch B
git add .
git commit -m "repo A: create 1st commit with some files (file A, file B)"
# 03. repo A: create branch branch1 from master
git branch branch1
# 04. clone the current repo (repo B)
cd ..
git clone A B
# 05. repo B, branch1: create 2nd commit containing new file (file C)
cd B
git checkout branch1
touch C
git add .
git commit -m "Second commit"
# 06. repo B: push changes to repo A
git push --repo ../A
# 07. repo A, branch1: modify line#1 in file C and commit
cd ../A
git checkout branch1
echo "repo A, branch1: modify line#1 in file C and commit" > C
git commit -am "repo A, branch1: modify line#1 in file C and commit"
# 08. repo B, branch1: modify line#1 in file C and commit
cd ../B
echo "repo B, branch1: modify line#1 in file C and commit" > C
git commit -am "repo B, branch1: modify line#1 in file C and commit"
# 09. repo B, branch1: fetch changes from repo A
git fetch origin branch1
# 10. repo B, branch1: merge's branch1 (resolve conflict)
git merge
echo "repo B, branch1: merge's branch1 (resolve conflict)" > C
git add .
git commit -m "repo B, branch1: merge's branch1 (resolve conflict)"
# 11. repo A: add repoB as new remote
cd ../A
git remote add B ../B
# 12. repo A, branch1: merge in repoB's branch1
git fetch B
git merge B/branch1
# Результат: 2 репы A, B + отдельная репа со списком всех команд
git remote add github https://github.com/KhasanovBI/A.git
git push github --all
cd ../B
git remote add github https://github.com/KhasanovBI/B.git
git push github --all
```

