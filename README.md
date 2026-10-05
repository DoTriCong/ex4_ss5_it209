# Bài 4: Mô phỏng quy trình Hotfix & Gitflow thực tế

## 1. Mục tiêu

Thực hành quy trình Gitflow khi phát hiện lỗi nghiêm trọng trên phiên bản production.

## 2. Các nhánh sử dụng

- main: chứa code production ổn định.
- develop: chứa code đang phát triển cho phiên bản tiếp theo.
- hotfix/v1.0.1: nhánh sửa lỗi khẩn cấp, được tạo trực tiếp từ main.

## 3. Quy trình thực hiện

### Bước 1: Tạo phiên bản production

Tạo commit ban đầu trên nhánh main với phiên bản 1.0.0.

### Bước 2: Tạo nhánh develop

Tạo nhánh develop từ main và phát triển tính năng mới.

### Bước 3: Tạo hotfix

Chuyển về main và tạo nhánh:

git switch -c hotfix/v1.0.1

Nhánh hotfix được tạo trực tiếp từ main.

### Bước 4: Sửa lỗi

Sửa lỗi bảo mật nghiêm trọng liên quan đến dữ liệu người dùng trên nhánh hotfix.

Commit:

git commit -m "Fix critical user data security issue"

### Bước 5: Merge hotfix vào main

Chuyển về main:

git switch main

Sau đó merge:

git merge hotfix/v1.0.1

### Bước 6: Tạo tag phiên bản

Tạo tag:

git tag -a v1.0.1 -m "Release Hotfix 1.0.1"

Tag v1.0.1 đánh dấu phiên bản release sau khi sửa lỗi.

### Bước 7: Merge hotfix về develop

Chuyển sang develop:

git switch develop

Sau đó:

git merge hotfix/v1.0.1

Việc merge ngược giúp mã nguồn trên develop cũng nhận được bản sửa lỗi bảo mật.

### Bước 8: Xóa nhánh hotfix

Sau khi hoàn thành việc merge:

git branch -d hotfix/v1.0.1

## 4. Sơ đồ Gitflow

main:
A -------- B
|
v1.0.1

develop:
A -------- C -------- D

hotfix:
B --------- H
/ \
/   \
main ---------------H     \
\
develop --------------------H

Trong đó:

A: Release version 1.0.0

C: Phát triển tính năng mới trên develop

H: Commit sửa lỗi khẩn cấp trên hotfix/v1.0.1

v1.0.1: Tag phiên bản release sau khi sửa lỗi.

## 5. Kiểm tra

Các lệnh kiểm tra:

git branch -a

git tag

git log --graph --oneline --all

Kết quả cho thấy tag v1.0.1 và lịch sử merge hotfix vào cả main và develop.

## 6. Kết luận

Quy trình hotfix giúp sửa lỗi nghiêm trọng trực tiếp trên phiên bản production mà không cần chờ các tính năng đang phát triển trên develop hoàn thành.

Sau khi sửa lỗi, hotfix được merge vào main để phát hành ngay và đồng thời merge ngược vào develop để tránh lỗi xuất hiện trở lại trong phiên bản tương lai.