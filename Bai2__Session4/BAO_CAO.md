# BÁO CÁO BÀI TẬP 2: QUẢN LÝ NHÁNH VÀ GIẢI QUYẾT XUNG ĐỘT (MERGE CONFLICT)

**Môn học:** IT_209 - Quản lý mã nguồn với Git  
**Bài tập:** Bài 2 - Session 04  
**Học viên thực hiện:** Hoang Cuong Cat (cathoangfb1@gmail.com)  
**Đường dẫn nộp bài trên GitHub:** `homework/session_04/ex2/`

---

## 1. Mục tiêu bài thực hành
- Tạo mới và chuyển đổi linh hoạt giữa các nhánh (branch) cục bộ: `main` và `feature-update`.
- Cố ý tạo tình huống xung đột gộp nhánh (Merge Conflict) trên cùng một dòng code ở tệp tin `README.md`.
- Xử lý xung đột thủ công thông qua việc giải thích và xóa bỏ các ký hiệu đánh dấu xung đột (`<<<<<<<`, `=======`, `>>>>>>>`).
- Hoàn thành commit gộp (Merge Commit) có 2 nhánh tổ tiên và hiểu rõ cơ chế gộp 3 vùng (3-Way Merge).

---

## 2. Các bước thực hiện chi tiết

### Bước 1: Khởi tạo repository và commit gốc trên nhánh `main`
- Khởi tạo Git repo với nhánh mặc định là `main`:
  ```bash
  git init -b main
  ```
- Tạo tệp `README.md` ban đầu với nội dung cơ bản:
  ```markdown
  # Dự án Quản lý Nhánh và Xử lý Xung Đột (Merge Conflict)

  ## Giới thiệu
  Đây là dự án thực hành Git Session 4 - Bài 2.

  ## Thông tin phiên bản
  Phiên bản hiện tại: v1.0.0 - Bản phát hành gốc trên nhánh main.

  ## Danh sách tính năng
  - Quản lý mã nguồn cơ bản
  ```
- Commit tệp `README.md` lên nhánh `main`:
  ```bash
  git add README.md
  git commit -m "Initial commit: Tạo file README.md ban đầu"
  ```
  *(Mã commit gốc: `eaa8a62`)*

---

### Bước 2: Tạo nhánh mới `feature-update` và chỉnh sửa file
- Tạo và chuyển sang nhánh `feature-update`:
  ```bash
  git checkout -b feature-update
  ```
- Cập nhật dòng thông tin phiên bản và tính năng mới trong `README.md`:
  ```markdown
  ## Thông tin phiên bản
  Phiên bản hiện tại: v1.1.0-feature - Cập nhật tính năng quản lý người dùng từ nhánh feature-update.

  ## Danh sách tính năng
  - Quản lý mã nguồn cơ bản
  - Quản lý người dùng (User Management - cập nhật từ feature-update)
  ```
- Commit thay đổi trên nhánh `feature-update`:
  ```bash
  git add README.md
  git commit -m "feat: cập nhật README.md với tính năng mới từ nhánh feature-update"
  ```
  *(Mã commit: `7563c42`)*

---

### Bước 3: Chuyển về nhánh `main` và chỉnh sửa cùng dòng mã
- Quay trở lại nhánh `main`:
  ```bash
  git checkout main
  ```
- Đồng thời cập nhật cùng các dòng trên trong `README.md` với bản vá nóng (hotfix):
  ```markdown
  ## Thông tin phiên bản
  Phiên bản hiện tại: v1.0.1 - Bản vá lỗi khẩn cấp (hotfix) trực tiếp trên nhánh main.

  ## Danh sách tính năng
  - Quản lý mã nguồn cơ bản
  - Bản vá bảo mật hệ thống (cập nhật từ main)
  ```
- Commit thay đổi trên nhánh `main`:
  ```bash
  git add README.md
  git commit -m "fix: cập nhật README.md với bản vá lỗi trực tiếp trên nhánh main"
  ```
  *(Mã commit: `40dd7b2`)*

---

### Bước 4: Thực hiện gộp nhánh và gây ra xung đột (Merge Conflict)
- Đứng tại nhánh `main`, thực hiện gộp nhánh `feature-update`:
  ```bash
  git merge feature-update
  ```
- Kết quả terminal trả về thông báo lỗi xung đột:
  ```
  Auto-merging README.md
  CONFLICT (content): Merge conflict in README.md
  Automatic merge failed; fix conflicts and then commit the result.
  ```

---

### Bước 5: Phân tích các dấu hiệu xung đột bên trong `README.md`
Khi mở tệp tin `README.md`, Git tự động đánh dấu vùng xung đột bằng các ký hiệu:
```markdown
<<<<<<< HEAD
Phiên bản hiện tại: v1.0.1 - Bản vá lỗi khẩn cấp (hotfix) trực tiếp trên nhánh main.

## Danh sách tính năng
- Quản lý mã nguồn cơ bản
- Bản vá bảo mật hệ thống (cập nhật từ main)
=======
Phiên bản hiện tại: v1.1.0-feature - Cập nhật tính năng quản lý người dùng từ nhánh feature-update.

## Danh sách tính năng
- Quản lý mã nguồn cơ bản
- Quản lý người dùng (User Management - cập nhật từ feature-update)
>>>>>>> feature-update
```

**Giải thích ý nghĩa các ký hiệu:**
- `<<<<<<< HEAD`: Bắt đầu vùng nội dung thuộc commit hiện tại trên nhánh đang đứng (`main`).
- `=======`: Đường phân cách giữa 2 phiên bản xung đột.
- `>>>>>>> feature-update`: Kết thúc vùng xung đột, nội dung phía trên thuộc nhánh đang được gộp vào (`feature-update`).

---

### Bước 6: Xử lý xung đột thủ công
- Học viên tiến hành xử lý thủ công:
  1. Loại bỏ hoàn toàn các dòng ký hiệu `<<<<<<< HEAD`, `=======`, `>>>>>>> feature-update`.
  2. Tích hợp hợp lý nội dung từ cả hai nhánh: Giữ lại cả tính năng quản lý người dùng từ nhánh phụ và bản vá bảo mật từ nhánh chính, nâng phiên bản lên `v1.1.0`.
- Nội dung file `README.md` sau khi giải quyết xung đột hoàn chỉnh:
  ```markdown
  # Dự án Quản lý Nhánh và Xử lý Xung Đột (Merge Conflict)

  ## Giới thiệu
  Đây là dự án thực hành Git Session 4 - Bài 2: Quản lý nhánh và giải quyết xung đột (Merge Conflict).

  ## Thông tin phiên bản
  Phiên bản hiện tại: v1.1.0 - Đã gộp thành công bản vá bảo mật từ nhánh main và tính năng quản lý người dùng từ nhánh feature-update.

  ## Danh sách tính năng
  - Quản lý mã nguồn cơ bản
  - Quản lý người dùng (User Management - tích hợp từ feature-update)
  - Bản vá bảo mật hệ thống (tích hợp từ hotfix main)
  ```

---

### Bước 7: Hoàn thành Commit Gộp (Merge Commit)
- Đánh dấu tệp đã giải quyết xung đột:
  ```bash
  git add README.md
  ```
- Hoàn tất commit gộp:
  ```bash
  git commit -m "Merge branch 'feature-update' into main: Giải quyết xung đột README.md"
  ```
  *(Mã commit: `79435c5`)*

---

## 3. Hiểu cơ chế gộp 3 vùng (3-Way Merge)
Trong bài thực hành này, Git sử dụng cơ chế **3-Way Merge** gồm 3 điểm mốc:
1. **Base Commit (Tổ tiên chung gần nhất):** Commit gốc `eaa8a62` trước khi nhánh `feature-update` được rẽ nhánh.
2. **Ours (Commit hiện tại):** Commit `40dd7b2` trên nhánh `main` (chứa bản vá bảo mật hotfix).
3. **Theirs (Commit nhánh đích):** Commit `7563c42` trên nhánh `feature-update` (chứa chức năng quản lý người dùng).

Do cả hai nhánh `main` và `feature-update` đều thay đổi cùng các dòng trong `README.md` so với Base Commit, Git không thể tự động quyết định giữ dòng nào nên yêu cầu lập trình viên giải quyết xung đột thủ công.

---

## 4. Kiểm tra kết quả đồ thị nhánh (git log --graph --oneline)

Thực thi lệnh kiểm tra:
```bash
git log --graph --oneline
```

**Kết quả đầu ra:**
```
*   79435c5 Merge branch 'feature-update' into main: Giải quyết xung đột README.md
|\  
| * 7563c42 feat: cập nhật README.md với tính năng mới từ nhánh feature-update
* | 40dd7b2 fix: cập nhật README.md với bản vá lỗi trực tiếp trên nhánh main
|/  
* eaa8a62 Initial commit: Tạo file README.md ban đầu
```

Lệnh kiểm tra đầy đủ nhãn (`--decorate --all`):
```bash
git log --graph --oneline --decorate --all
```
**Kết quả đầu ra:**
```
*   79435c5 (HEAD -> main) Merge branch 'feature-update' into main: Giải quyết xung đột README.md
|\  
| * 7563c42 (feature-update) feat: cập nhật README.md với tính năng mới từ nhánh feature-update
* | 40dd7b2 fix: cập nhật README.md với bản vá lỗi trực tiếp trên nhánh main
|/  
* eaa8a62 Initial commit: Tạo file README.md ban đầu
```

> **Nhận xét kết quả:** Đồ thị hiển thị trực quan nhánh `feature-update` được tách ra từ `main` tại commit `eaa8a62`, phát triển song song với `main`, sau đó được gộp lại tại commit `79435c5` với đầy đủ 2 nhánh tổ tiên, thỏa mãn 100% yêu cầu đề bài.
