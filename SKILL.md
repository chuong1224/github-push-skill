-----
## name: github-push
version: 2.0.0
description: Kich hoat khi user muon tao repo moi tren GitHub, push file hoac code len GitHub, setup README dep, them badge, lam README song ngu Anh-Viet, them Version History. BAT CU KHI NAO user noi: “push to github”, “tao repo va push”, “github push”, “push len github”, “create github repo”, “setup github”, “push skill to github”, “tao repo github”, “create repo”, “push code”. Vi du: “Tao repo github cho skill nay va push len”, “push cai nay len github voi readme song ngu”, “setup github repo cho project nay”. Khong kich hoat khi user chi hoi ve kien thuc git, hoi ve GitHub Actions, hoac khong co y dinh thuc su tao hoac push len repo.

# GitHub Push

Tao repo GitHub moi + push code/files + setup README chuyen nghiep chi bang vai cau tu nhien.
Output: repo sach, README dep song ngu, badge day du, san sang su dung ngay.

## Workflow chinh

### Buoc 1 — Xac dinh yeu cau

Kiem tra context tu user. Neu thieu, hoi toi thieu:

- Ten repo mong muon (chua co → goi y kebab-case tu ten project)
- Mo ta ngan gon cua project (1 dong)
- Loai project (chon 1): Grok Skill | Web App | Library | Script | Other
- Public hay Private? (mac dinh: Public)

Khong hoi nhung gi user da noi ro.

### Buoc 2 — Tao repository

Goi tool `github___create_repository` voi:

|Tham so    |Gia tri            |
|-----------|-------------------|
|name       |ten-repo-kebab-case|
|description|mo ta ngan         |
|private    |false (mac dinh)   |
|autoInit   |true               |

Neu repo da ton tai → hoi user co muon push vao repo do khong.

### Buoc 3 — Tao noi dung files

Chuan bi truoc khi push:

|File          |Dieu kien tao                                        |
|--------------|-----------------------------------------------------|
|README.md     |Luon co — song ngu Anh-Viet + badge + Version History|
|LICENSE       |Tao MIT mac dinh (hoi neu user co preference khac)   |
|.gitignore    |Tao phu hop voi loai project da xac dinh o Buoc 1    |
|SKILL.md      |Chi tao neu loai project la Grok Skill               |
|File code khac|Chi tao neu user cung cap noi dung cu the            |

### Buoc 4 — Viet README song ngu chuan

Cau truc README bat buoc theo thu tu nay:

```
[Badge row]

# Ten Project

> Mo ta 1 dong bang tieng Anh

---

## English
### Overview
### Features
### Installation
### Usage
### License

---

## Tieng Viet
### Tong quan
### Tinh nang
### Cai dat
### Huong dan su dung
### Giay phep

---

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0.0 | YYYY-MM-DD | Initial release |
```

Badge chuan (them theo loai project):

|Badge                     |Loai project ap dung|
|--------------------------|--------------------|
|Version (shields.io/badge)|Tat ca              |
|License: MIT              |Tat ca              |
|Last Commit               |Tat ca              |
|Stars (social)            |Tat ca              |
|Grok Skill (custom badge) |Chi Grok Skill      |
|Build Status              |Web App / Library   |

### Buoc 5 — Push files

Su dung `github___push_files` de push tat ca files cung luc.

Commit message mac dinh: `feat: initial setup with bilingual README and badges`

Neu push mot file rieng le → dung `github___create_or_update_file`.

### Buoc 6 — Hoan tat

- Tra link repo day du (https://github.com/username/repo-name)
- Hoi co muon them khong: release, topics, GitHub Pages, v.v.

## Gotchas

|#|Van de hay gap                                                      |Cach xu ly                                                                                           |
|-|--------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
|1|User chua connect GitHub MCP                                        |Nhac connect GitHub account trong Settings truoc khi chay skill                                      |
|2|Ten repo bi trung hoac co ky tu khong hop le                        |De xuat ten thay the (kebab-case, chi dung a-z, 0-9, dau gach ngang)                                 |
|3|User cung cap file SKILL.md → quen mention trong README             |Tu dong them “Includes SKILL.md” vao Features section khi loai project la Grok Skill                 |
|4|README qua dai vi dich tung dong                                    |Viet English section day du truoc, sau do tom tat Vietnamese (khong phai dich word-by-word)          |
|5|push_files that bai vi autoInit: false tao repo rong khong co commit|Kiem tra autoInit: true khi goi create_repository; neu repo cu khong co commit → tao README gia truoc|
|6|User muon push vao repo da co san                                   |Hoi ten repo + username, dung create_or_update_file thay vi create_repository                        |
|7|Badge URL sai vi repo chua public hoac chua co release              |Dung shields.io/badge voi gia tri hardcode cho version, khong dung dynamic badge cho repo moi        |
|8|Commit message khong ro rang                                        |Luon dung Conventional Commits: feat/fix/docs/chore + mo ta ngan                                     |