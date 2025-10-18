# MÔ TẢ CHI TIẾT CÁC BẢNG DATABASE

## Bảng USERS (Người dùng)

| Tên cột       | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                |
| ------------- | ------------------------ | ------------ | --------- | ------------------------------------------------------ |
| id            | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                          |
| username      | Tên đăng nhập            | VARCHAR      | 50        | Duy nhất (UNIQUE), Không rỗng (NOT NULL)               |
| email         | Địa chỉ email            | VARCHAR      | 100       | Duy nhất (UNIQUE), Không rỗng (NOT NULL)               |
| password_hash | Mã hóa mật khẩu          | VARCHAR      | 255       | Không rỗng (NOT NULL)                                  |
| full_name     | Họ và tên đầy đủ         | VARCHAR      | 100       | Không rỗng (NOT NULL)                                  |
| phone         | Số điện thoại            | VARCHAR      | 20        |                                                        |
| address       | Địa chỉ                  | TEXT         |           |                                                        |
| date_of_birth | Ngày sinh                | DATE         |           |                                                        |
| gender        | Giới tính                | ENUM         |           | ('male', 'female', 'other')                            |
| avatar_url    | URL ảnh đại diện         | VARCHAR      | 255       |                                                        |
| is_active     | Trạng thái hoạt động     | BOOLEAN      |           | Mặc định TRUE                                          |
| created_at    | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                             |
| updated_at    | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

## Bảng ROLES (Vai trò)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                  |
| ----------- | ------------------------ | ------------ | --------- | ---------------------------------------- |
| id          | Khóa chính (PRIMARY KEY) | INT          |           | Tự động tăng (AUTO_INCREMENT)            |
| name        | Tên vai trò              | VARCHAR      | 50        | Duy nhất (UNIQUE), Không rỗng (NOT NULL) |
| description | Mô tả vai trò            | TEXT         |           |                                          |
| created_at  | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP               |

## Bảng PERMISSIONS (Quyền hạn)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                  |
| ----------- | ------------------------ | ------------ | --------- | ---------------------------------------- |
| id          | Khóa chính (PRIMARY KEY) | INT          |           | Tự động tăng (AUTO_INCREMENT)            |
| name        | Tên quyền hạn            | VARCHAR      | 100       | Duy nhất (UNIQUE), Không rỗng (NOT NULL) |
| description | Mô tả quyền hạn          | TEXT         |           |                                          |
| resource    | Tài nguyên               | VARCHAR      | 50        | Không rỗng (NOT NULL)                    |
| action      | Hành động                | VARCHAR      | 50        | Không rỗng (NOT NULL)                    |
| created_at  | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP               |

## Bảng USER_ROLES (Liên kết Người dùng-Vai trò)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                              |
| ----------- | ------------------------ | ------------ | --------- | -------------------------------------------------------------------- |
| id          | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                        |
| user_id     | ID người dùng            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES users(id) |
| role_id     | ID vai trò               | INT          |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES roles(id) |
| assigned_at | Thời gian gán            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                           |
| assigned_by | Người gán                | BIGINT       |           | Khóa ngoại (FOREIGN KEY) REFERENCES users(id)                        |

## Bảng ROLE_PERMISSIONS (Liên kết Vai trò-Quyền hạn)

| Tên cột       | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                    |
| ------------- | ------------------------ | ------------ | --------- | -------------------------------------------------------------------------- |
| id            | Khóa chính (PRIMARY KEY) | INT          |           | Tự động tăng (AUTO_INCREMENT)                                              |
| role_id       | ID vai trò               | INT          |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES roles(id)       |
| permission_id | ID quyền hạn             | INT          |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES permissions(id) |

## Bảng CUSTOMERS (Khách hàng)

| Tên cột                    | Giải thích                      | Kiểu dữ liệu | Maxlength | Ghi chú                                                              |
| -------------------------- | ------------------------------- | ------------ | --------- | -------------------------------------------------------------------- |
| id                         | Khóa chính (PRIMARY KEY)        | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                        |
| user_id                    | ID người dùng                   | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES users(id) |
| customer_code              | Mã khách hàng                   | VARCHAR      | 20        | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                             |
| membership_rank            | Cấp độ thành viên               | ENUM         |           | ('bronze', 'silver', 'gold', 'platinum'), Mặc định 'bronze'          |
| total_spent                | Tổng chi tiêu                   | DECIMAL      |           | (15,2), Mặc định 0                                                   |
| loyalty_points             | Điểm tích lũy                   | INT          |           | Mặc định 0                                                           |
| preferred_payment_method   | Phương thức thanh toán ưa thích | VARCHAR      | 50        |                                                                      |
| preferred_shipping_address | Địa chỉ giao hàng ưa thích      | TEXT         |           |                                                                      |
| is_vip                     | Khách hàng VIP                  | BOOLEAN      |           | Mặc định FALSE                                                       |
| created_at                 | Thời gian tạo                   | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                           |
| updated_at                 | Thời gian cập nhật              | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP               |

## Bảng CUSTOMER_ADDRESSES (Địa chỉ Khách hàng)

| Tên cột       | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                  |
| ------------- | ------------------------ | ------------ | --------- | ------------------------------------------------------------------------ |
| id            | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                            |
| customer_id   | ID khách hàng            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES customers(id) |
| address_type  | Loại địa chỉ             | ENUM         |           | ('home', 'work', 'other'), Mặc định 'home'                               |
| full_name     | Họ và tên đầy đủ         | VARCHAR      | 100       | Không rỗng (NOT NULL)                                                    |
| phone         | Số điện thoại            | VARCHAR      | 20        | Không rỗng (NOT NULL)                                                    |
| address_line1 | Địa chỉ dòng 1           | VARCHAR      | 255       | Không rỗng (NOT NULL)                                                    |
| address_line2 | Địa chỉ dòng 2           | VARCHAR      | 255       |                                                                          |
| city          | Thành phố                | VARCHAR      | 100       | Không rỗng (NOT NULL)                                                    |
| district      | Quận/Huyện               | VARCHAR      | 100       | Không rỗng (NOT NULL)                                                    |
| ward          | Phường/Xã                | VARCHAR      | 100       | Không rỗng (NOT NULL)                                                    |
| postal_code   | Mã bưu điện              | VARCHAR      | 20        |                                                                          |
| is_default    | Địa chỉ mặc định         | BOOLEAN      |           | Mặc định FALSE                                                           |
| created_at    | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                               |
| updated_at    | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP                   |

## Bảng CATEGORIES (Danh mục)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                |
| ----------- | ------------------------ | ------------ | --------- | ------------------------------------------------------ |
| id          | Khóa chính (PRIMARY KEY) | INT          |           | Tự động tăng (AUTO_INCREMENT)                          |
| name        | Tên danh mục             | VARCHAR      | 100       | Không rỗng (NOT NULL)                                  |
| description | Mô tả danh mục           | TEXT         |           |                                                        |
| parent_id   | ID danh mục cha          | INT          |           | Khóa ngoại (FOREIGN KEY) REFERENCES categories(id)     |
| image_url   | URL hình ảnh             | VARCHAR      | 255       |                                                        |
| is_active   | Trạng thái hoạt động     | BOOLEAN      |           | Mặc định TRUE                                          |
| sort_order  | Thứ tự sắp xếp           | INT          |           | Mặc định 0                                             |
| created_at  | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                             |
| updated_at  | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

## Bảng AUTHORS (Tác giả)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                |
| ----------- | ------------------------ | ------------ | --------- | ------------------------------------------------------ |
| id          | Khóa chính (PRIMARY KEY) | INT          |           | Tự động tăng (AUTO_INCREMENT)                          |
| name        | Tên tác giả              | VARCHAR      | 100       | Không rỗng (NOT NULL)                                  |
| biography   | Tiểu sử                  | TEXT         |           |                                                        |
| birth_date  | Ngày sinh                | DATE         |           |                                                        |
| nationality | Quốc tịch                | VARCHAR      | 50        |                                                        |
| image_url   | URL hình ảnh             | VARCHAR      | 255       |                                                        |
| created_at  | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                             |
| updated_at  | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

## Bảng PUBLISHERS (Nhà xuất bản)

| Tên cột      | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                |
| ------------ | ------------------------ | ------------ | --------- | ------------------------------------------------------ |
| id           | Khóa chính (PRIMARY KEY) | INT          |           | Tự động tăng (AUTO_INCREMENT)                          |
| name         | Tên nhà xuất bản         | VARCHAR      | 100       | Không rỗng (NOT NULL)                                  |
| description  | Mô tả                    | TEXT         |           |                                                        |
| website      | Website                  | VARCHAR      | 255       |                                                        |
| contact_info | Thông tin liên hệ        | TEXT         |           |                                                        |
| created_at   | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                             |
| updated_at   | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

## Bảng BOOKS (Sách)

| Tên cột             | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                |
| ------------------- | ------------------------ | ------------ | --------- | ---------------------------------------------------------------------- |
| id                  | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                          |
| isbn                | Mã ISBN                  | VARCHAR      | 20        | Duy nhất (UNIQUE)                                                      |
| title               | Tên sách                 | VARCHAR      | 255       | Không rỗng (NOT NULL)                                                  |
| subtitle            | Tên phụ                  | VARCHAR      | 255       |                                                                        |
| description         | Mô tả sách               | TEXT         |           |                                                                        |
| content             | Nội dung sách            | TEXT         |           |                                                                        |
| page_count          | Số trang                 | INT          |           |                                                                        |
| publication_date    | Ngày xuất bản            | DATE         |           |                                                                        |
| language            | Ngôn ngữ                 | VARCHAR      | 50        | Mặc định 'Vietnamese'                                                  |
| format              | Định dạng                | ENUM         |           | ('hardcover', 'paperback', 'ebook', 'audiobook'), Mặc định 'paperback' |
| dimensions          | Kích thước               | VARCHAR      | 50        |                                                                        |
| weight              | Trọng lượng              | DECIMAL      |           | (8,2)                                                                  |
| price               | Giá bán                  | DECIMAL      |           | (10,2), Không rỗng (NOT NULL)                                          |
| original_price      | Giá gốc                  | DECIMAL      |           | (10,2)                                                                 |
| discount_percentage | Phần trăm giảm giá       | DECIMAL      |           | (5,2), Mặc định 0                                                      |
| category_id         | ID danh mục              | INT          |           | Khóa ngoại (FOREIGN KEY) REFERENCES categories(id)                     |
| publisher_id        | ID nhà xuất bản          | INT          |           | Khóa ngoại (FOREIGN KEY) REFERENCES publishers(id)                     |
| cover_image_url     | URL ảnh bìa              | VARCHAR      | 255       |                                                                        |
| sample_content      | Nội dung mẫu             | TEXT         |           |                                                                        |
| is_active           | Trạng thái hoạt động     | BOOLEAN      |           | Mặc định TRUE                                                          |
| is_featured         | Sách nổi bật             | BOOLEAN      |           | Mặc định FALSE                                                         |
| stock_quantity      | Số lượng tồn kho         | INT          |           | Mặc định 0                                                             |
| min_stock_level     | Mức tồn kho tối thiểu    | INT          |           | Mặc định 5                                                             |
| max_stock_level     | Mức tồn kho tối đa       | INT          |           | Mặc định 1000                                                          |
| created_at          | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                             |
| updated_at          | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP                 |

## Bảng BOOK_AUTHORS (Liên kết Sách-Tác giả)

| Tên cột   | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                |
| --------- | ------------------------ | ------------ | --------- | ---------------------------------------------------------------------- |
| id        | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                          |
| book_id   | ID sách                  | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES books(id)   |
| author_id | ID tác giả               | INT          |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES authors(id) |
| role      | Vai trò                  | ENUM         |           | ('author', 'co-author', 'translator', 'editor'), Mặc định 'author'     |

## Bảng BOOK_IMAGES (Hình ảnh Sách)

| Tên cột    | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                              |
| ---------- | ------------------------ | ------------ | --------- | -------------------------------------------------------------------- |
| id         | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                        |
| book_id    | ID sách                  | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES books(id) |
| image_url  | URL hình ảnh             | VARCHAR      | 255       | Không rỗng (NOT NULL)                                                |
| alt_text   | Văn bản thay thế         | VARCHAR      | 255       |                                                                      |
| sort_order | Thứ tự sắp xếp           | INT          |           | Mặc định 0                                                           |
| is_primary | Ảnh chính                | BOOLEAN      |           | Mặc định FALSE                                                       |
| created_at | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                           |

## Bảng WAREHOUSES (Kho hàng)

| Tên cột    | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                |
| ---------- | ------------------------ | ------------ | --------- | ------------------------------------------------------ |
| id         | Khóa chính (PRIMARY KEY) | INT          |           | Tự động tăng (AUTO_INCREMENT)                          |
| name       | Tên kho                  | VARCHAR      | 100       | Không rỗng (NOT NULL)                                  |
| address    | Địa chỉ kho              | TEXT         |           | Không rỗng (NOT NULL)                                  |
| manager_id | ID quản lý               | BIGINT       |           | Khóa ngoại (FOREIGN KEY) REFERENCES users(id)          |
| capacity   | Sức chứa                 | INT          |           |                                                        |
| is_active  | Trạng thái hoạt động     | BOOLEAN      |           | Mặc định TRUE                                          |
| created_at | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                             |
| updated_at | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

## Bảng INVENTORY (Tồn kho)

| Tên cột            | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                   |
| ------------------ | ------------------------ | ------------ | --------- | ------------------------------------------------------------------------- |
| id                 | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                             |
| book_id            | ID sách                  | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES books(id)      |
| warehouse_id       | ID kho                   | INT          |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES warehouses(id) |
| quantity           | Số lượng tồn kho         | INT          |           | Không rỗng (NOT NULL), Mặc định 0                                         |
| reserved_quantity  | Số lượng đã đặt          | INT          |           | Mặc định 0                                                                |
| available_quantity | Số lượng có sẵn          | INT          |           | GENERATED ALWAYS AS (quantity - reserved_quantity) STORED                 |
| last_updated       | Lần cập nhật cuối        | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP                    |

## Bảng INVENTORY_HISTORY (Lịch sử Tồn kho)

| Tên cột          | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                             |
| ---------------- | ------------------------ | ------------ | --------- | ----------------------------------------------------------------------------------- |
| id               | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                                       |
| book_id          | ID sách                  | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES books(id)                |
| warehouse_id     | ID kho                   | INT          |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES warehouses(id)           |
| transaction_type | Loại giao dịch           | ENUM         |           | ('import', 'export', 'adjustment', 'reserved', 'unreserved'), Không rỗng (NOT NULL) |
| quantity_change  | Thay đổi số lượng        | INT          |           | Không rỗng (NOT NULL)                                                               |
| quantity_before  | Số lượng trước           | INT          |           | Không rỗng (NOT NULL)                                                               |
| quantity_after   | Số lượng sau             | INT          |           | Không rỗng (NOT NULL)                                                               |
| reason           | Lý do                    | VARCHAR      | 255       |                                                                                     |
| reference_id     | ID tham chiếu            | BIGINT       |           |                                                                                     |
| reference_type   | Loại tham chiếu          | VARCHAR      | 50        |                                                                                     |
| created_by       | Người tạo                | BIGINT       |           | Khóa ngoại (FOREIGN KEY) REFERENCES users(id)                                       |
| created_at       | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                                          |

## Bảng CART_ITEMS (Chi tiết Giỏ hàng)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                  |
| ----------- | ------------------------ | ------------ | --------- | ------------------------------------------------------------------------ |
| id          | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                            |
| customer_id | ID khách hàng            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES customers(id) |
| book_id     | ID sách                  | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES books(id)     |
| quantity    | Số lượng                 | INT          |           | Không rỗng (NOT NULL), Mặc định 1                                        |
| added_at    | Thời gian thêm           | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                               |
| updated_at  | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP                   |

## Bảng WISHLIST_ITEMS (Chi tiết Danh sách yêu thích)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                  |
| ----------- | ------------------------ | ------------ | --------- | ------------------------------------------------------------------------ |
| id          | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                            |
| customer_id | ID khách hàng            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES customers(id) |
| book_id     | ID sách                  | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES books(id)     |
| added_at    | Thời gian thêm           | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                               |

## Bảng ORDERS (Đơn hàng)

| Tên cột          | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                                                     |
| ---------------- | ------------------------ | ------------ | --------- | ----------------------------------------------------------------------------------------------------------- |
| id               | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                                                               |
| order_code       | Mã đơn hàng              | VARCHAR      | 20        | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                                                                    |
| customer_id      | ID khách hàng            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES customers(id)                                    |
| order_type       | Loại đơn hàng            | ENUM         |           | ('online', 'offline'), Mặc định 'online'                                                                    |
| status           | Trạng thái đơn hàng      | ENUM         |           | ('pending', 'confirmed', 'preparing', 'shipping', 'delivered', 'cancelled', 'returned'), Mặc định 'pending' |
| payment_status   | Trạng thái thanh toán    | ENUM         |           | ('pending', 'paid', 'failed', 'refunded'), Mặc định 'pending'                                               |
| shipping_status  | Trạng thái vận chuyển    | ENUM         |           | ('pending', 'preparing', 'shipped', 'delivered', 'returned'), Mặc định 'pending'                            |
| subtotal         | Tổng tiền phụ            | DECIMAL      |           | (15,2), Không rỗng (NOT NULL)                                                                               |
| discount_amount  | Số tiền giảm giá         | DECIMAL      |           | (15,2), Mặc định 0                                                                                          |
| shipping_fee     | Phí vận chuyển           | DECIMAL      |           | (15,2), Mặc định 0                                                                                          |
| tax_amount       | Số tiền thuế             | DECIMAL      |           | (15,2), Mặc định 0                                                                                          |
| total_amount     | Tổng tiền                | DECIMAL      |           | (15,2), Không rỗng (NOT NULL)                                                                               |
| payment_method   | Phương thức thanh toán   | VARCHAR      | 50        |                                                                                                             |
| shipping_address | Địa chỉ giao hàng        | TEXT         |           | Không rỗng (NOT NULL)                                                                                       |
| billing_address  | Địa chỉ thanh toán       | TEXT         |           |                                                                                                             |
| notes            | Ghi chú                  | TEXT         |           |                                                                                                             |
| priority         | Mức độ ưu tiên           | ENUM         |           | ('low', 'medium', 'high', 'urgent'), Mặc định 'medium'                                                      |
| created_by       | Người tạo                | BIGINT       |           | Khóa ngoại (FOREIGN KEY) REFERENCES users(id)                                                               |
| created_at       | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                                                                  |
| updated_at       | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP                                                      |

## Bảng ORDER_ITEMS (Chi tiết Đơn hàng)

| Tên cột             | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                               |
| ------------------- | ------------------------ | ------------ | --------- | --------------------------------------------------------------------- |
| id                  | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                         |
| order_id            | ID đơn hàng              | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES orders(id) |
| book_id             | ID sách                  | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES books(id)  |
| quantity            | Số lượng                 | INT          |           | Không rỗng (NOT NULL)                                                 |
| unit_price          | Giá đơn vị               | DECIMAL      |           | (10,2), Không rỗng (NOT NULL)                                         |
| discount_percentage | Phần trăm giảm giá       | DECIMAL      |           | (5,2), Mặc định 0                                                     |
| total_price         | Tổng tiền                | DECIMAL      |           | (15,2), Không rỗng (NOT NULL)                                         |

## Bảng PAYMENTS (Thanh toán)

| Tên cột          | Giải thích                  | Kiểu dữ liệu | Maxlength | Ghi chú                                                                                       |
| ---------------- | --------------------------- | ------------ | --------- | --------------------------------------------------------------------------------------------- |
| id               | Khóa chính (PRIMARY KEY)    | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                                                 |
| order_id         | ID đơn hàng                 | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES orders(id)                         |
| payment_method   | Phương thức thanh toán      | VARCHAR      | 50        | Không rỗng (NOT NULL)                                                                         |
| payment_status   | Trạng thái thanh toán       | ENUM         |           | ('pending', 'processing', 'completed', 'failed', 'cancelled', 'refunded'), Mặc định 'pending' |
| amount           | Số tiền                     | DECIMAL      |           | (15,2), Không rỗng (NOT NULL)                                                                 |
| transaction_id   | ID giao dịch                | VARCHAR      | 100       |                                                                                               |
| gateway_response | Phản hồi từ cổng thanh toán | TEXT         |           |                                                                                               |
| paid_at          | Thời gian thanh toán        | TIMESTAMP    |           |                                                                                               |
| created_at       | Thời gian tạo               | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                                                    |
| updated_at       | Thời gian cập nhật          | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP                                        |

## Bảng SHIPPING_PROVIDERS (Đơn vị Vận chuyển)

| Tên cột      | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                |
| ------------ | ------------------------ | ------------ | --------- | ------------------------------------------------------ |
| id           | Khóa chính (PRIMARY KEY) | INT          |           | Tự động tăng (AUTO_INCREMENT)                          |
| name         | Tên đơn vị vận chuyển    | VARCHAR      | 100       | Không rỗng (NOT NULL)                                  |
| code         | Mã đơn vị                | VARCHAR      | 20        | Duy nhất (UNIQUE), Không rỗng (NOT NULL)               |
| contact_info | Thông tin liên hệ        | TEXT         |           |                                                        |
| is_active    | Trạng thái hoạt động     | BOOLEAN      |           | Mặc định TRUE                                          |
| created_at   | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                             |
| updated_at   | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

## Bảng SHIPMENTS (Vận chuyển)

| Tên cột                 | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                                       |
| ----------------------- | ------------------------ | ------------ | --------- | --------------------------------------------------------------------------------------------- |
| id                      | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                                                 |
| order_id                | ID đơn hàng              | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES orders(id)                         |
| shipping_provider_id    | ID đơn vị vận chuyển     | INT          |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES shipping_providers(id)             |
| tracking_number         | Số theo dõi              | VARCHAR      | 100       |                                                                                               |
| status                  | Trạng thái vận chuyển    | ENUM         |           | ('pending', 'picked_up', 'in_transit', 'delivered', 'failed', 'returned'), Mặc định 'pending' |
| shipping_fee            | Phí vận chuyển           | DECIMAL      |           | (10,2), Không rỗng (NOT NULL)                                                                 |
| estimated_delivery_date | Ngày giao dự kiến        | DATE         |           |                                                                                               |
| actual_delivery_date    | Ngày giao thực tế        | DATE         |           |                                                                                               |
| notes                   | Ghi chú                  | TEXT         |           |                                                                                               |
| created_at              | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                                                    |
| updated_at              | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP                                        |

## Bảng SHIPMENT_HISTORY (Lịch sử Vận chuyển)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                                          |
| ----------- | ------------------------ | ------------ | --------- | ------------------------------------------------------------------------------------------------ |
| id          | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                                                    |
| shipment_id | ID vận chuyển            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES shipments(id)                         |
| status      | Trạng thái               | ENUM         |           | ('pending', 'picked_up', 'in_transit', 'delivered', 'failed', 'returned'), Không rỗng (NOT NULL) |
| location    | Vị trí                   | VARCHAR      | 255       |                                                                                                  |
| description | Mô tả                    | TEXT         |           |                                                                                                  |
| created_at  | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                                                       |

## Bảng DISCOUNT_CODES (Mã giảm giá)

| Tên cột             | Giải thích                 | Kiểu dữ liệu | Maxlength | Ghi chú                                                |
| ------------------- | -------------------------- | ------------ | --------- | ------------------------------------------------------ |
| id                  | Khóa chính (PRIMARY KEY)   | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                          |
| code                | Mã giảm giá                | VARCHAR      | 50        | Duy nhất (UNIQUE), Không rỗng (NOT NULL)               |
| name                | Tên mã giảm giá            | VARCHAR      | 100       | Không rỗng (NOT NULL)                                  |
| description         | Mô tả                      | TEXT         |           |                                                        |
| discount_type       | Loại giảm giá              | ENUM         |           | ('percentage', 'fixed_amount'), Không rỗng (NOT NULL)  |
| discount_value      | Giá trị giảm giá           | DECIMAL      |           | (10,2), Không rỗng (NOT NULL)                          |
| min_order_amount    | Số tiền đơn hàng tối thiểu | DECIMAL      |           | (15,2)                                                 |
| max_discount_amount | Số tiền giảm tối đa        | DECIMAL      |           | (15,2)                                                 |
| usage_limit         | Giới hạn sử dụng           | INT          |           |                                                        |
| used_count          | Số lần đã sử dụng          | INT          |           | Mặc định 0                                             |
| is_active           | Trạng thái hoạt động       | BOOLEAN      |           | Mặc định TRUE                                          |
| valid_from          | Có hiệu lực từ             | TIMESTAMP    |           | Không rỗng (NOT NULL)                                  |
| valid_until         | Có hiệu lực đến            | TIMESTAMP    |           | Không rỗng (NOT NULL)                                  |
| created_by          | Người tạo                  | BIGINT       |           | Khóa ngoại (FOREIGN KEY) REFERENCES users(id)          |
| created_at          | Thời gian tạo              | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                             |
| updated_at          | Thời gian cập nhật         | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

## Bảng DISCOUNT_CODE_USAGE (Sử dụng Mã giảm giá)

| Tên cột          | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                       |
| ---------------- | ------------------------ | ------------ | --------- | ----------------------------------------------------------------------------- |
| id               | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                                 |
| discount_code_id | ID mã giảm giá           | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES discount_codes(id) |
| order_id         | ID đơn hàng              | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES orders(id)         |
| customer_id      | ID khách hàng            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES customers(id)      |
| discount_amount  | Số tiền giảm giá         | DECIMAL      |           | (15,2), Không rỗng (NOT NULL)                                                 |
| used_at          | Thời gian sử dụng        | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                                    |

## Bảng BOOK_REVIEWS (Đánh giá Sách)

| Tên cột       | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                  |
| ------------- | ------------------------ | ------------ | --------- | ------------------------------------------------------------------------ |
| id            | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                            |
| book_id       | ID sách                  | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES books(id)     |
| customer_id   | ID khách hàng            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES customers(id) |
| order_id      | ID đơn hàng              | BIGINT       |           | Khóa ngoại (FOREIGN KEY) REFERENCES orders(id)                           |
| rating        | Đánh giá                 | INT          |           | Không rỗng (NOT NULL), CHECK (rating >= 1 AND rating <= 5)               |
| title         | Tiêu đề đánh giá         | VARCHAR      | 255       |                                                                          |
| content       | Nội dung đánh giá        | TEXT         |           |                                                                          |
| is_verified   | Đã xác minh              | BOOLEAN      |           | Mặc định FALSE                                                           |
| is_approved   | Đã phê duyệt             | BOOLEAN      |           | Mặc định TRUE                                                            |
| helpful_count | Số lượt hữu ích          | INT          |           | Mặc định 0                                                               |
| created_at    | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                               |
| updated_at    | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP                   |

## Bảng REVIEW_HELPFULNESS (Đánh giá Hữu ích)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                     |
| ----------- | ------------------------ | ------------ | --------- | --------------------------------------------------------------------------- |
| id          | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                               |
| review_id   | ID đánh giá              | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES book_reviews(id) |
| customer_id | ID khách hàng            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES customers(id)    |
| is_helpful  | Hữu ích                  | BOOLEAN      |           | Không rỗng (NOT NULL)                                                       |
| created_at  | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                                  |

## Bảng NOTIFICATIONS (Thông báo)

| Tên cột    | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                              |
| ---------- | ------------------------ | ------------ | --------- | -------------------------------------------------------------------- |
| id         | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                        |
| user_id    | ID người dùng            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES users(id) |
| title      | Tiêu đề                  | VARCHAR      | 255       | Không rỗng (NOT NULL)                                                |
| content    | Nội dung                 | TEXT         |           | Không rỗng (NOT NULL)                                                |
| type       | Loại thông báo           | ENUM         |           | ('info', 'warning', 'success', 'error'), Mặc định 'info'             |
| category   | Danh mục                 | ENUM         |           | ('order', 'promotion', 'security', 'system'), Mặc định 'system'      |
| is_read    | Đã đọc                   | BOOLEAN      |           | Mặc định FALSE                                                       |
| read_at    | Thời gian đọc            | TIMESTAMP    |           |                                                                      |
| created_at | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                           |

## Bảng SUPPORT_TICKETS (Phiếu hỗ trợ)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                  |
| ----------- | ------------------------ | ------------ | --------- | ------------------------------------------------------------------------ |
| id          | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                            |
| ticket_code | Mã phiếu hỗ trợ          | VARCHAR      | 20        | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                                 |
| customer_id | ID khách hàng            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES customers(id) |
| subject     | Chủ đề                   | VARCHAR      | 255       | Không rỗng (NOT NULL)                                                    |
| description | Mô tả                    | TEXT         |           | Không rỗng (NOT NULL)                                                    |
| priority    | Mức độ ưu tiên           | ENUM         |           | ('low', 'medium', 'high', 'urgent'), Mặc định 'medium'                   |
| status      | Trạng thái               | ENUM         |           | ('open', 'in_progress', 'resolved', 'closed'), Mặc định 'open'           |
| assigned_to | Người được giao          | BIGINT       |           | Khóa ngoại (FOREIGN KEY) REFERENCES users(id)                            |
| created_at  | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                               |
| updated_at  | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP                   |

## Bảng SUPPORT_MESSAGES (Tin nhắn Hỗ trợ)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                        |
| ----------- | ------------------------ | ------------ | --------- | ------------------------------------------------------------------------------ |
| id          | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                                  |
| ticket_id   | ID phiếu hỗ trợ          | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES support_tickets(id) |
| sender_id   | ID người gửi             | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES users(id)           |
| message     | Nội dung tin nhắn        | TEXT         |           | Không rỗng (NOT NULL)                                                          |
| is_internal | Tin nhắn nội bộ          | BOOLEAN      |           | Mặc định FALSE                                                                 |
| created_at  | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                                     |

## Bảng USER_SESSIONS (Phiên đăng nhập)

| Tên cột       | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                              |
| ------------- | ------------------------ | ------------ | --------- | -------------------------------------------------------------------- |
| id            | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                        |
| user_id       | ID người dùng            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES users(id) |
| session_token | Token phiên              | VARCHAR      | 255       | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                             |
| ip_address    | Địa chỉ IP               | VARCHAR      | 45        |                                                                      |
| user_agent    | User Agent               | TEXT         |           |                                                                      |
| device_info   | Thông tin thiết bị       | VARCHAR      | 255       |                                                                      |
| is_active     | Trạng thái hoạt động     | BOOLEAN      |           | Mặc định TRUE                                                        |
| last_activity | Hoạt động cuối           | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP               |
| created_at    | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                           |
| expires_at    | Thời gian hết hạn        | TIMESTAMP    |           | Không rỗng (NOT NULL)                                                |

## Bảng LOGIN_HISTORY (Lịch sử đăng nhập)

| Tên cột          | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                              |
| ---------------- | ------------------------ | ------------ | --------- | -------------------------------------------------------------------- |
| id               | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                        |
| user_id          | ID người dùng            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES users(id) |
| ip_address       | Địa chỉ IP               | VARCHAR      | 45        |                                                                      |
| user_agent       | User Agent               | TEXT         |           |                                                                      |
| login_successful | Đăng nhập thành công     | BOOLEAN      |           | Không rỗng (NOT NULL)                                                |
| failure_reason   | Lý do thất bại           | VARCHAR      | 255       |                                                                      |
| created_at       | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                           |

## Bảng SYSTEM_LOGS (Nhật ký hệ thống)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                   |
| ----------- | ------------------------ | ------------ | --------- | --------------------------------------------------------- |
| id          | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                             |
| user_id     | ID người dùng            | BIGINT       |           | Khóa ngoại (FOREIGN KEY) REFERENCES users(id)             |
| action      | Hành động                | VARCHAR      | 100       | Không rỗng (NOT NULL)                                     |
| resource    | Tài nguyên               | VARCHAR      | 50        | Không rỗng (NOT NULL)                                     |
| resource_id | ID tài nguyên            | BIGINT       |           |                                                           |
| description | Mô tả                    | TEXT         |           |                                                           |
| ip_address  | Địa chỉ IP               | VARCHAR      | 45        |                                                           |
| user_agent  | User Agent               | TEXT         |           |                                                           |
| level       | Mức độ                   | ENUM         |           | ('info', 'warning', 'error', 'critical'), Mặc định 'info' |
| created_at  | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                |

## Bảng IMPORT_REQUESTS (Yêu cầu nhập hàng)

| Tên cột            | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                              |
| ------------------ | ------------------------ | ------------ | --------- | -------------------------------------------------------------------- |
| id                 | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                        |
| request_code       | Mã yêu cầu               | VARCHAR      | 20        | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                             |
| book_id            | ID sách                  | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES books(id) |
| requested_by       | Người yêu cầu            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES users(id) |
| requested_quantity | Số lượng yêu cầu         | INT          |           | Không rỗng (NOT NULL)                                                |
| reason             | Lý do                    | TEXT         |           |                                                                      |
| priority           | Mức độ ưu tiên           | ENUM         |           | ('low', 'medium', 'high', 'urgent'), Mặc định 'medium'               |
| status             | Trạng thái               | ENUM         |           | ('pending', 'approved', 'rejected', 'completed'), Mặc định 'pending' |
| approved_by        | Người phê duyệt          | BIGINT       |           | Khóa ngoại (FOREIGN KEY) REFERENCES users(id)                        |
| approved_at        | Thời gian phê duyệt      | TIMESTAMP    |           |                                                                      |
| rejection_reason   | Lý do từ chối            | TEXT         |           |                                                                      |
| created_at         | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                           |
| updated_at         | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP               |

## Bảng RETURN_REQUESTS (Yêu cầu đổi trả)

| Tên cột      | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                  |
| ------------ | ------------------------ | ------------ | --------- | ------------------------------------------------------------------------ |
| id           | Khóa chính (PRIMARY KEY) | BIGINT       |           | Tự động tăng (AUTO_INCREMENT)                                            |
| request_code | Mã yêu cầu               | VARCHAR      | 20        | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                                 |
| order_id     | ID đơn hàng              | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES orders(id)    |
| customer_id  | ID khách hàng            | BIGINT       |           | Không rỗng (NOT NULL), Khóa ngoại (FOREIGN KEY) REFERENCES customers(id) |
| reason       | Lý do                    | TEXT         |           | Không rỗng (NOT NULL)                                                    |
| status       | Trạng thái               | ENUM         |           | ('pending', 'approved', 'rejected', 'completed'), Mặc định 'pending'     |
| processed_by | Người xử lý              | BIGINT       |           | Khóa ngoại (FOREIGN KEY) REFERENCES users(id)                            |
| processed_at | Thời gian xử lý          | TIMESTAMP    |           |                                                                          |
| notes        | Ghi chú                  | TEXT         |           |                                                                          |
| created_at   | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP                                               |
| updated_at   | Thời gian cập nhật       | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP                   |

## Bảng WORKFLOW_TRANSITIONS (Chuyển đổi Workflow)

| Tên cột             | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                       |
| ------------------- | ------------------------ | ------------ | --------- | ----------------------------- |
| id                  | Khóa chính (PRIMARY KEY) | INT          |           | Tự động tăng (AUTO_INCREMENT) |
| resource_type       | Loại tài nguyên          | VARCHAR      | 50        | Không rỗng (NOT NULL)         |
| from_status         | Trạng thái từ            | VARCHAR      | 50        | Không rỗng (NOT NULL)         |
| to_status           | Trạng thái đến           | VARCHAR      | 50        | Không rỗng (NOT NULL)         |
| required_role       | Vai trò yêu cầu          | VARCHAR      | 50        |                               |
| required_permission | Quyền hạn yêu cầu        | VARCHAR      | 100       |                               |
| is_active           | Trạng thái hoạt động     | BOOLEAN      |           | Mặc định TRUE                 |
| created_at          | Thời gian tạo            | TIMESTAMP    |           | Mặc định CURRENT_TIMESTAMP    |
