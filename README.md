<!-- CI CD -->
npm install -> npm run dev -> Trong file package.json: Sửa dòng code: "test": "jest --watch" thành "test": "jest --coverage" -> npm run test
B1) Vào dự án Github
B2) Trên thanh menu -> Chọn Actions -> Do ta đẩy dự án với môi trường nodejs (react, angular, next, vue,...) nên ta sẽ chọn Node.js (By Github Actions) (Build and test a Node.js with npm) -> Bấm Configure (Đây là những workflows đã được xây dựng sẵn, nhiệm vụ của chúng ta là sử dụng lại)
B3) Chỉnh sửa lại nội dung của file .yml
B4) Nhìn qua bên tay phải góc trên -> Bấm Commit changes... -> Nó sẽ hiển thị lên 1 popup Commit changes. Điền Commit message -> Bấm Commit changes
B5) Lúc này trên thanh menu mục Actions đã xuất hiện workflows của chúng ta (Đồng thời trong source code của chúng ta cũng xuất hiện 1 folder như sau: .github/workflows)

Cấu hình nếu như có bất kỳ 1 job nào bị failed trong quá trình chạy CI CD thì chúng ta sẽ Disabled cái nút Merge pull request (Trên thanh menu -> Mục Pull requests)
B1) Trên thanh menu -> Chọn Settings
B2) Bên thanh sidebars -> Chọn Branches -> Bấm Add branch protection rule -> Đặt cái branch mà ta muốn setup protection trong Branch name pattern (main)
B3) Chúng ta không muốn ai cũng có thể push code trực tiếp lên branch chính của mình là branch main. Trong Protect matching branches -> Tick chọn:
- Require a pull request before merging (Bắt buộc phải tạo pull request nếu muốn merge code vào branch main)
- Require a status check to pass before merging (Kiểm tra các cái status hay chính là các cái job của chúng ta xem có cài nào bị failed hay không. Tất cả các cái job phải pass hết thì mới được merge)
Ở mục Search for status checks in the last week for this repository: Nhập tên của các cái job mà ta muốn đảm bảo là nó phải pass (thành công) vô 
VD: 
build (16.x)
build (18.x)
Bấm Create