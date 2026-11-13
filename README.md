# ketoanupdate

Repo **công khai** chỉ dùng cho cơ chế tự cập nhật của phần mềm Quản lý Hoá đơn.

Chứa:
- `version.json` — manifest phiên bản mới nhất (máy khách đọc qua raw.githubusercontent.com).
- Release assets — file `DichVuCongThue.exe` của từng phiên bản.

Mã nguồn nằm ở repo riêng (private) `solo-code-com/ketoan`.

## Phát hành phiên bản mới

```powershell
python build.py
python publish_release.py --version 1.0.1 --notes "Nội dung thay đổi"
gh release create v1.0.1 "dist\DichVuCongThue.exe" --repo solo-code-com/ketoanupdate -t v1.0.1 -n "v1.0.1"
cd update_repo
git add version.json
git commit -m "release: v1.0.1"
git push
```

Manifest: https://raw.githubusercontent.com/solo-code-com/ketoanupdate/main/version.json
