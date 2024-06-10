<!-- CI CD -->
# npm install -> npm run dev -> Trong file package.json: Sửa dòng code: "test": "jest --watch" thành "test": "jest --coverage" -> npm run test
B1) Vào dự án Github
B2) Trên thanh menu -> Chọn Actions -> Do ta đẩy dự án với môi trường nodejs (react, angular, next, vue,...) nên ta sẽ chọn Node.js (By Github Actions) (Build and test a Node.js with npm) -> Bấm Configure (Đây là những workflows đã được xây dựng sẵn, nhiệm vụ của chúng ta là sử dụng lại)
B3) Chỉnh sửa lại nội dung của file .yml
B4) Nhìn qua bên tay phải góc trên -> Bấm Commit changes... -> Nó sẽ hiển thị lên 1 popup Commit changes. Điền Commit message -> Bấm Commit changes
B5) Lúc này trên thanh menu mục Actions đã xuất hiện workflow của chúng ta (Đồng thời trong source code của chúng ta cũng xuất hiện 1 folder như sau: .github/workflows kèm với file node.js.yml)

# Cấu hình nếu như có bất kỳ 1 job nào bị failed trong quá trình chạy CI CD thì chúng ta sẽ Disabled cái nút Merge pull request (Trên thanh menu -> Mục Pull requests)
B1) Trên thanh menu -> Chọn Settings
B2) Bên thanh sidebars -> Chọn Branches -> Bấm Add branch protection rule -> Đặt cái branch mà ta muốn setup protection trong Branch name pattern (main)
B3) Chúng ta không muốn ai cũng có thể push code trực tiếp lên branch chính của mình là branch main. Trong Protect matching branches -> Tick chọn:
- Require a pull request before merging (Untick (bỏ check) Require approvals) (Bắt buộc phải tạo pull request nếu muốn merge code vào branch main)
- Require status checks to pass before merging (Kiểm tra các cái status hay chính là các cái job của chúng ta xem có cài nào bị failed hay không. Tất cả các cái job phải pass hết thì mới được merge)
Ở mục Search for status checks in the last week for this repository: Nhập tên của các cái job mà ta muốn đảm bảo là nó phải pass (thành công) vô 
VD: 
build (16.x)
build (18.x)
Bấm Create

# Hướng dẫn tích hợp deploy lên github page
B1) Trên thanh menu -> Chọn Settings
B2) Bên thanh sidebars -> Chọn Pages -> Tại trang GitHub Pages, tìm đến mục Build and deployment, mục Source chọn GitHub Actions. Lúc này nó sẽ xuất hiện gợi ý chúng ta sử dụng workflow của nextjs với các thông tin như sau:
Next.js (By GitHub Actions) (Package a Next.js site.)
(Nằm dưới dòng Use a suggested workflow, browse all workflows, or create your own.)
Bấm Configure
B3) Chỉnh sửa lại nội dung của file .yml
Sửa từ:
on:
  push:
    branches: ["main"]
Thành: 
on:
  push:
    branches: ["production"]
B4) Nhìn qua bên tay phải góc trên -> Bấm Commit changes... -> Nó sẽ hiển thị lên 1 popup Commit changes. Điền Commit message -> Bấm Propose changes
B5) Lúc này nó sẽ tự tạo 1 pull request vào nhánh main của chúng ta từ một nhánh được tạo bởi github (vd: branch tên là nguyenkien12345/nguyenkien12345-patch-2). Bấm Create pull request
B6) Lúc này trên thanh menu mục Actions chúng ta sẽ kiểm tra xem cái workflow vừa được thực thi lại có thành công hay không (Do chúng ta vừa tạo pull request nên nó sẽ thực thi lại workflow không quan tâm pull request này đã được merged hay chưa)
B7) Trên thanh menu -> Chọn Pull requests. Nhấn vào cái pull request mà chúng ta vừa tạo ở trên. Lúc này chúng ta sẽ thấy tiêu đề All checks have passed (Kèm với tick xanh) đồng thời nút Merge pull request không còn bị disable nữa (Hiển thị màu xanh lá cây) => Bấm Merge pull request => Bấm Confirm merge => Sau khi merge xong hiển thị Pull request successfully merged and closed
B8) Lúc này trên thanh menu mục Actions đã xuất hiện workflow mới của chúng ta với title là Merge pull request #2 from nguyenkien12345/nguyenkien12345-patch-2 và kiểm tra xem là workflow này có chạy thành công hay không
(Đồng thời trong source code của chúng ta cũng xuất hiện 1 file mới là nextjs.yml trong folder .github/workflows)
B9) Do dự án này sẽ chỉ được đẩy lên Github Pages thông qua nhánh production (Chúng ta setup ở Bước 3 trong nội dung của file nextjs.yml) nên chúng ta sẽ tạo nhánh production từ nhánh main. Sau đó push nhánh production này lên trên dự repository của chúng ta là xong
B10) Lúc này trên thanh menu mục Actions sau khi chạy lại workflow nó sẽ báo lỗi: Branch "production" is not allowed to deploy to github-pages due to environment protection rules. Do trước đó chúng ta đã cấu hình trong Branches (Trên thanh menu -> Chọn Settings => Bên thanh sidebars -> Chọn Branches) chúng ta chỉ cho phép mỗi branch main được thực thi. Lúc này chúng ta cũng phải setup tương tự cho branch production
B11) Trên thanh menu -> Chọn Settings
B12) Bên thanh sidebars -> Chọn Branches -> Bấm Add branch protection rule -> Đặt cái branch mà ta muốn setup protection trong Branch name pattern (production)
B13) Chúng ta không muốn ai cũng có thể push code trực tiếp lên branch chính của mình là branch production. Trong Protect matching branches -> Tick chọn:
- Require a pull request before merging (Untick (bỏ check) Require approvals) (Bắt buộc phải tạo pull request nếu muốn merge code vào branch main)
- Require status checks to pass before merging (Kiểm tra các cái status hay chính là các cái job của chúng ta xem có cài nào bị failed hay không. Tất cả các cái job phải pass hết thì mới được merge)
Ở mục Search for status checks in the last week for this repository: Nhập tên của các cái job mà ta muốn đảm bảo là nó phải pass (thành công) vô 
VD: 
build (16.x)
build (18.x)
Bấm Create
B14) Trên thanh menu -> Chọn Actions. Bên thanh sidebars (Có title là Actions) mục All workflows, chọn cái workflow có tiêu đề là Deploy Next.js site to Pages. Lúc này thay vì phải tạo một pull request mới vào nhánh production chúng ta sẽ thực thi manual (thủ công bằng tay). Bấm Run workflow => Bấm Run workflow