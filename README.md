# MÔ TẢ CHI TIẾT CÁC BẢNG DATABASE

## Bảng USERS (Người dùng)

| Tên cột        | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                               |
| -------------- | ------------------------ | ------------ | --------- | ------------------------------------------------------------------------------------- |
| id             | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                                               |
| email          | Địa chỉ email            | VARCHAR      | 255       | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                                              |
| password_hash  | Mã hóa mật khẩu          | VARCHAR      | 255       | Không rỗng (NOT NULL)                                                                 |
| full_name      | Họ và tên đầy đủ         | VARCHAR      | 255       | Không rỗng (NOT NULL)                                                                 |
| phone          | Số điện thoại            | VARCHAR      | 20        |                                                                                       |
| avatar_url     | URL ảnh đại diện         | TEXT         |           |                                                                                       |
| date_of_birth  | Ngày sinh                | DATE         |           |                                                                                       |
| gender         | Giới tính                | VARCHAR      | 10        | CHECK (gender IN ('male', 'female', 'other'))                                         |
| address        | Địa chỉ                  | TEXT         |           |                                                                                       |
| city           | Thành phố                | VARCHAR      | 100       |                                                                                       |
| district       | Quận/Huyện               | VARCHAR      | 100       |                                                                                       |
| ward           | Phường/Xã                | VARCHAR      | 100       |                                                                                       |
| postal_code    | Mã bưu điện              | VARCHAR      | 20        |                                                                                       |
| role           | Vai trò                  | VARCHAR      | 20        | NOT NULL, DEFAULT 'user', CHECK (role IN ('user', 'admin', 'staff', 'warehouse'))     |
| status         | Trạng thái tài khoản     | VARCHAR      | 20        | NOT NULL, DEFAULT 'active', CHECK (status IN ('active', 'inactive', 'banned'))        |
| email_verified | Xác thực email           | BOOLEAN      |           | DEFAULT FALSE                                                                         |
| phone_verified | Xác thực số điện thoại   | BOOLEAN      |           | DEFAULT FALSE                                                                         |
| last_login     | Lần đăng nhập cuối       | TIMESTAMP    |           |                                                                                       |
| total_orders   | Tổng số đơn hàng         | INTEGER      |           | DEFAULT 0                                                                             |
| total_spent    | Tổng số tiền đã chi      | DECIMAL      | 15,2      | DEFAULT 0                                                                             |
| rank           | Cấp độ thành viên        | VARCHAR      | 20        | DEFAULT 'Bronze', CHECK (rank IN ('Bronze', 'Silver', 'Gold', 'Platinum', 'Diamond')) |
| points         | Điểm tích lũy            | INTEGER      |           | DEFAULT 0                                                                             |
| created_at     | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                             |
| updated_at     | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                             |

## Bảng USER_SESSIONS (Phiên đăng nhập)

| Tên cột       | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                     |
| ------------- | ------------------------ | ------------ | --------- | ------------------------------------------- |
| id            | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())     |
| user_id       | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id) |
| session_token | Token phiên đăng nhập    | VARCHAR      | 255       | Duy nhất (UNIQUE), Không rỗng (NOT NULL)    |
| device_info   | Thông tin thiết bị       | TEXT         |           |                                             |
| ip_address    | Địa chỉ IP               | INET         |           |                                             |
| user_agent    | Thông tin trình duyệt    | TEXT         |           |                                             |
| is_active     | Trạng thái hoạt động     | BOOLEAN      |           | DEFAULT TRUE                                |
| expires_at    | Thời gian hết hạn        | TIMESTAMP    |           | Không rỗng (NOT NULL)                       |
| created_at    | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                   |
| last_activity | Lần hoạt động cuối       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                   |

## Bảng LOGIN_HISTORY (Lịch sử đăng nhập)

| Tên cột        | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                     |
| -------------- | ------------------------ | ------------ | --------- | ------------------------------------------- |
| id             | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())     |
| user_id        | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id) |
| login_time     | Thời gian đăng nhập      | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                   |
| ip_address     | Địa chỉ IP               | INET         |           |                                             |
| user_agent     | Thông tin trình duyệt    | TEXT         |           |                                             |
| device_info    | Thông tin thiết bị       | TEXT         |           |                                             |
| success        | Trạng thái thành công    | BOOLEAN      |           | Không rỗng (NOT NULL)                       |
| failure_reason | Lý do thất bại           | VARCHAR      | 255       |                                             |

## Bảng CATEGORIES (Danh mục sản phẩm)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                  |
| ----------- | ------------------------ | ------------ | --------- | ---------------------------------------- |
| id          | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())  |
| name        | Tên danh mục             | VARCHAR      | 255       | Không rỗng (NOT NULL)                    |
| slug        | URL slug                 | VARCHAR      | 255       | Duy nhất (UNIQUE), Không rỗng (NOT NULL) |
| description | Mô tả danh mục           | TEXT         |           |                                          |
| image_url   | URL hình ảnh danh mục    | TEXT         |           |                                          |
| parent_id   | ID danh mục cha          | UUID         |           | Tham chiếu categories(id)                |
| sort_order  | Thứ tự sắp xếp           | INTEGER      |           | DEFAULT 0                                |
| is_active   | Trạng thái hoạt động     | BOOLEAN      |           | DEFAULT TRUE                             |
| created_at  | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                |
| updated_at  | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                |

## Bảng BRANDS (Thương hiệu)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                  |
| ----------- | ------------------------ | ------------ | --------- | ---------------------------------------- |
| id          | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())  |
| name        | Tên thương hiệu          | VARCHAR      | 255       | Không rỗng (NOT NULL)                    |
| slug        | URL slug                 | VARCHAR      | 255       | Duy nhất (UNIQUE), Không rỗng (NOT NULL) |
| logo_url    | URL logo thương hiệu     | TEXT         |           |                                          |
| description | Mô tả thương hiệu        | TEXT         |           |                                          |
| website     | Website thương hiệu      | VARCHAR      | 255       |                                          |
| is_active   | Trạng thái hoạt động     | BOOLEAN      |           | DEFAULT TRUE                             |
| created_at  | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                |
| updated_at  | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                |

## Bảng PRODUCTS (Sản phẩm)

| Tên cột              | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                            |
| -------------------- | ------------------------ | ------------ | --------- | ---------------------------------------------------------------------------------- |
| id                   | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                                            |
| name                 | Tên sản phẩm             | VARCHAR      | 255       | Không rỗng (NOT NULL)                                                              |
| slug                 | URL slug                 | VARCHAR      | 255       | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                                           |
| description          | Mô tả sản phẩm           | TEXT         |           |                                                                                    |
| short_description    | Mô tả ngắn               | TEXT         |           |                                                                                    |
| category_id          | ID danh mục              | UUID         |           | Không rỗng (NOT NULL), Tham chiếu categories(id)                                   |
| brand_id             | ID thương hiệu           | UUID         |           | Không rỗng (NOT NULL), Tham chiếu brands(id)                                       |
| series               | Tên series               | VARCHAR      | 255       |                                                                                    |
| scale                | Tỷ lệ mô hình            | VARCHAR      | 50        |                                                                                    |
| material             | Chất liệu                | VARCHAR      | 100       |                                                                                    |
| dimensions           | Kích thước               | VARCHAR      | 100       |                                                                                    |
| weight               | Trọng lượng              | DECIMAL      | 8,2       |                                                                                    |
| price                | Giá bán                  | DECIMAL      | 15,2      | Không rỗng (NOT NULL)                                                              |
| original_price       | Giá gốc                  | DECIMAL      | 15,2      |                                                                                    |
| cost_price           | Giá nhập                 | DECIMAL      | 15,2      |                                                                                    |
| sku                  | Mã sản phẩm              | VARCHAR      | 100       | Duy nhất (UNIQUE)                                                                  |
| barcode              | Mã vạch                  | VARCHAR      | 100       |                                                                                    |
| status               | Trạng thái sản phẩm      | VARCHAR      | 20        | DEFAULT 'draft', CHECK (status IN ('draft', 'active', 'inactive', 'discontinued')) |
| is_featured          | Sản phẩm nổi bật         | BOOLEAN      |           | DEFAULT FALSE                                                                      |
| is_pre_order         | Sản phẩm đặt trước       | BOOLEAN      |           | DEFAULT FALSE                                                                      |
| pre_order_start_date | Ngày bắt đầu đặt trước   | TIMESTAMP    |           |                                                                                    |
| pre_order_end_date   | Ngày kết thúc đặt trước  | TIMESTAMP    |           |                                                                                    |
| release_date         | Ngày phát hành           | DATE         |           |                                                                                    |
| stock_quantity       | Số lượng tồn kho         | INTEGER      |           | DEFAULT 0                                                                          |
| min_stock_level      | Mức tồn kho tối thiểu    | INTEGER      |           | DEFAULT 0                                                                          |
| max_stock_level      | Mức tồn kho tối đa       | INTEGER      |           | DEFAULT 0                                                                          |
| weight_kg            | Trọng lượng (kg)         | DECIMAL      | 8,2       |                                                                                    |
| dimensions_cm        | Kích thước (cm)          | VARCHAR      | 50        |                                                                                    |
| tags                 | Thẻ tag                  | TEXT[]       |           | Mảng text                                                                          |
| meta_title           | Tiêu đề SEO              | VARCHAR      | 255       |                                                                                    |
| meta_description     | Mô tả SEO                | TEXT         |           |                                                                                    |
| created_by           | Người tạo                | UUID         |           | Tham chiếu users(id)                                                               |
| updated_by           | Người cập nhật           | UUID         |           | Tham chiếu users(id)                                                               |
| created_at           | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                          |
| updated_at           | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                          |

## Bảng PRODUCT_IMAGES (Hình ảnh sản phẩm)

| Tên cột    | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                        |
| ---------- | ------------------------ | ------------ | --------- | ---------------------------------------------- |
| id         | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())        |
| product_id | ID sản phẩm              | UUID         |           | Không rỗng (NOT NULL), Tham chiếu products(id) |
| image_url  | URL hình ảnh             | TEXT         |           | Không rỗng (NOT NULL)                          |
| alt_text   | Văn bản thay thế         | VARCHAR      | 255       |                                                |
| sort_order | Thứ tự sắp xếp           | INTEGER      |           | DEFAULT 0                                      |
| is_primary | Hình ảnh chính           | BOOLEAN      |           | DEFAULT FALSE                                  |
| created_at | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                      |

## Bảng PRODUCT_VARIANTS (Biến thể sản phẩm)

| Tên cột        | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                        |
| -------------- | ------------------------ | ------------ | --------- | ---------------------------------------------- |
| id             | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())        |
| product_id     | ID sản phẩm              | UUID         |           | Không rỗng (NOT NULL), Tham chiếu products(id) |
| name           | Tên biến thể             | VARCHAR      | 255       | Không rỗng (NOT NULL)                          |
| sku            | Mã biến thể              | VARCHAR      | 100       | Duy nhất (UNIQUE)                              |
| price          | Giá biến thể             | DECIMAL      | 15,2      |                                                |
| stock_quantity | Số lượng tồn kho         | INTEGER      |           | DEFAULT 0                                      |
| attributes     | Thuộc tính biến thể      | JSONB        |           | {color: "red", size: "M"}                      |
| is_active      | Trạng thái hoạt động     | BOOLEAN      |           | DEFAULT TRUE                                   |
| created_at     | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                      |
| updated_at     | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                      |

## Bảng INVENTORY (Tồn kho)

| Tên cột            | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                        |
| ------------------ | ------------------------ | ------------ | --------- | ---------------------------------------------- |
| id                 | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())        |
| product_id         | ID sản phẩm              | UUID         |           | Không rỗng (NOT NULL), Tham chiếu products(id) |
| variant_id         | ID biến thể              | UUID         |           | Tham chiếu product_variants(id)                |
| warehouse_location | Vị trí kho               | VARCHAR      | 100       |                                                |
| quantity_available | Số lượng có sẵn          | INTEGER      |           | Không rỗng (NOT NULL), DEFAULT 0               |
| quantity_reserved  | Số lượng đã đặt          | INTEGER      |           | Không rỗng (NOT NULL), DEFAULT 0               |
| quantity_sold      | Số lượng đã bán          | INTEGER      |           | Không rỗng (NOT NULL), DEFAULT 0               |
| min_stock_level    | Mức tồn kho tối thiểu    | INTEGER      |           | DEFAULT 0                                      |
| max_stock_level    | Mức tồn kho tối đa       | INTEGER      |           | DEFAULT 0                                      |
| reorder_point      | Điểm đặt hàng lại        | INTEGER      |           | DEFAULT 0                                      |
| last_restocked     | Lần nhập kho cuối        | TIMESTAMP    |           |                                                |
| last_audit         | Lần kiểm kê cuối         | TIMESTAMP    |           |                                                |
| created_at         | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                      |
| updated_at         | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                      |

## Bảng INVENTORY_TRANSACTIONS (Giao dịch tồn kho)

| Tên cột           | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                                    |
| ----------------- | ------------------------ | ------------ | --------- | ------------------------------------------------------------------------------------------ |
| id                | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                                                    |
| product_id        | ID sản phẩm              | UUID         |           | Không rỗng (NOT NULL), Tham chiếu products(id)                                             |
| variant_id        | ID biến thể              | UUID         |           | Tham chiếu product_variants(id)                                                            |
| transaction_type  | Loại giao dịch           | VARCHAR      | 20        | Không rỗng (NOT NULL), CHECK (transaction_type IN ('in', 'out', 'adjustment', 'transfer')) |
| quantity          | Số lượng                 | INTEGER      |           | Không rỗng (NOT NULL)                                                                      |
| previous_quantity | Số lượng trước đó        | INTEGER      |           | Không rỗng (NOT NULL)                                                                      |
| new_quantity      | Số lượng mới             | INTEGER      |           | Không rỗng (NOT NULL)                                                                      |
| reason            | Lý do giao dịch          | VARCHAR      | 255       |                                                                                            |
| reference_id      | ID tham chiếu            | UUID         |           | ID của đơn hàng, phiếu nhập, etc.                                                          |
| reference_type    | Loại tham chiếu          | VARCHAR      | 50        | 'order', 'import', 'adjustment', etc.                                                      |
| created_by        | Người tạo                | UUID         |           | Tham chiếu users(id)                                                                       |
| created_at        | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                                  |

## Bảng STOCK_ALERTS (Cảnh báo tồn kho)

| Tên cột            | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                                 |
| ------------------ | ------------------------ | ------------ | --------- | --------------------------------------------------------------------------------------- |
| id                 | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                                                 |
| product_id         | ID sản phẩm              | UUID         |           | Không rỗng (NOT NULL), Tham chiếu products(id)                                          |
| alert_type         | Loại cảnh báo            | VARCHAR      | 20        | Không rỗng (NOT NULL), CHECK (alert_type IN ('low_stock', 'out_of_stock', 'overstock')) |
| current_quantity   | Số lượng hiện tại        | INTEGER      |           | Không rỗng (NOT NULL)                                                                   |
| threshold_quantity | Số lượng ngưỡng          | INTEGER      |           | Không rỗng (NOT NULL)                                                                   |
| is_resolved        | Đã giải quyết            | BOOLEAN      |           | DEFAULT FALSE                                                                           |
| resolved_at        | Thời gian giải quyết     | TIMESTAMP    |           |                                                                                         |
| resolved_by        | Người giải quyết         | UUID         |           | Tham chiếu users(id)                                                                    |
| created_at         | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                               |

## Bảng CART (Giỏ hàng)

| Tên cột    | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                     |
| ---------- | ------------------------ | ------------ | --------- | ------------------------------------------- |
| id         | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())     |
| user_id    | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id) |
| session_id | ID phiên làm việc        | VARCHAR      | 255       | Cho khách vãng lai                          |
| created_at | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                   |
| updated_at | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                   |

## Bảng CART_ITEMS (Sản phẩm trong giỏ hàng)

| Tên cột    | Giải thích                     | Kiểu dữ liệu | Maxlength | Ghi chú                                        |
| ---------- | ------------------------------ | ------------ | --------- | ---------------------------------------------- |
| id         | Khóa chính (PRIMARY KEY)       | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())        |
| cart_id    | ID giỏ hàng                    | UUID         |           | Không rỗng (NOT NULL), Tham chiếu cart(id)     |
| product_id | ID sản phẩm                    | UUID         |           | Không rỗng (NOT NULL), Tham chiếu products(id) |
| variant_id | ID biến thể                    | UUID         |           | Tham chiếu product_variants(id)                |
| quantity   | Số lượng                       | INTEGER      |           | Không rỗng (NOT NULL), DEFAULT 1               |
| price      | Giá tại thời điểm thêm vào giỏ | DECIMAL      | 15,2      | Không rỗng (NOT NULL)                          |
| created_at | Thời gian tạo                  | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                      |
| updated_at | Thời gian cập nhật             | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                      |

## Bảng ORDERS (Đơn hàng)

| Tên cột              | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                                                                                 |
| -------------------- | ------------------------ | ------------ | --------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| id                   | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                                                                                                 |
| order_number         | Số đơn hàng              | VARCHAR      | 50        | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                                                                                                |
| user_id              | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id)                                                                                             |
| status               | Trạng thái đơn hàng      | VARCHAR      | 20        | NOT NULL, DEFAULT 'pending', CHECK (status IN ('pending', 'confirmed', 'processing', 'shipping', 'delivered', 'cancelled', 'returned')) |
| payment_status       | Trạng thái thanh toán    | VARCHAR      | 20        | NOT NULL, DEFAULT 'pending', CHECK (payment_status IN ('pending', 'paid', 'failed', 'refunded', 'partially_refunded'))                  |
| shipping_status      | Trạng thái vận chuyển    | VARCHAR      | 20        | NOT NULL, DEFAULT 'pending', CHECK (shipping_status IN ('pending', 'preparing', 'shipped', 'delivered', 'returned'))                    |
| shipping_name        | Tên người nhận           | VARCHAR      | 255       | Không rỗng (NOT NULL)                                                                                                                   |
| shipping_phone       | Số điện thoại người nhận | VARCHAR      | 20        | Không rỗng (NOT NULL)                                                                                                                   |
| shipping_address     | Địa chỉ giao hàng        | TEXT         |           | Không rỗng (NOT NULL)                                                                                                                   |
| shipping_city        | Thành phố giao hàng      | VARCHAR      | 100       | Không rỗng (NOT NULL)                                                                                                                   |
| shipping_district    | Quận/Huyện giao hàng     | VARCHAR      | 100       | Không rỗng (NOT NULL)                                                                                                                   |
| shipping_ward        | Phường/Xã giao hàng      | VARCHAR      | 100       | Không rỗng (NOT NULL)                                                                                                                   |
| shipping_postal_code | Mã bưu điện giao hàng    | VARCHAR      | 20        |                                                                                                                                         |
| payment_method       | Phương thức thanh toán   | VARCHAR      | 50        | Không rỗng (NOT NULL)                                                                                                                   |
| payment_reference    | Mã tham chiếu thanh toán | VARCHAR      | 255       |                                                                                                                                         |
| shipping_method      | Phương thức vận chuyển   | VARCHAR      | 100       |                                                                                                                                         |
| shipping_fee         | Phí vận chuyển           | DECIMAL      | 15,2      | DEFAULT 0                                                                                                                               |
| tracking_number      | Mã vận đơn               | VARCHAR      | 100       |                                                                                                                                         |
| carrier              | Đơn vị vận chuyển        | VARCHAR      | 100       |                                                                                                                                         |
| subtotal             | Tổng tiền hàng           | DECIMAL      | 15,2      | Không rỗng (NOT NULL)                                                                                                                   |
| tax_amount           | Số tiền thuế             | DECIMAL      | 15,2      | DEFAULT 0                                                                                                                               |
| discount_amount      | Số tiền giảm giá         | DECIMAL      | 15,2      | DEFAULT 0                                                                                                                               |
| shipping_fee_amount  | Số tiền phí vận chuyển   | DECIMAL      | 15,2      | DEFAULT 0                                                                                                                               |
| total_amount         | Tổng cộng                | DECIMAL      | 15,2      | Không rỗng (NOT NULL)                                                                                                                   |
| customer_notes       | Ghi chú khách hàng       | TEXT         |           |                                                                                                                                         |
| admin_notes          | Ghi chú admin            | TEXT         |           |                                                                                                                                         |
| order_date           | Ngày đặt hàng            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                                                                               |
| confirmed_at         | Thời gian xác nhận       | TIMESTAMP    |           |                                                                                                                                         |
| shipped_at           | Thời gian giao hàng      | TIMESTAMP    |           |                                                                                                                                         |
| delivered_at         | Thời gian nhận hàng      | TIMESTAMP    |           |                                                                                                                                         |
| cancelled_at         | Thời gian hủy            | TIMESTAMP    |           |                                                                                                                                         |
| created_at           | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                                                                               |
| updated_at           | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                                                                               |

## Bảng ORDER_ITEMS (Chi tiết đơn hàng)

| Tên cột      | Giải thích                     | Kiểu dữ liệu | Maxlength | Ghi chú                                        |
| ------------ | ------------------------------ | ------------ | --------- | ---------------------------------------------- |
| id           | Khóa chính (PRIMARY KEY)       | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())        |
| order_id     | ID đơn hàng                    | UUID         |           | Không rỗng (NOT NULL), Tham chiếu orders(id)   |
| product_id   | ID sản phẩm                    | UUID         |           | Không rỗng (NOT NULL), Tham chiếu products(id) |
| variant_id   | ID biến thể                    | UUID         |           | Tham chiếu product_variants(id)                |
| product_name | Tên sản phẩm tại thời điểm đặt | VARCHAR      | 255       | Không rỗng (NOT NULL)                          |
| product_sku  | Mã sản phẩm tại thời điểm đặt  | VARCHAR      | 100       |                                                |
| quantity     | Số lượng                       | INTEGER      |           | Không rỗng (NOT NULL)                          |
| unit_price   | Đơn giá                        | DECIMAL      | 15,2      | Không rỗng (NOT NULL)                          |
| total_price  | Thành tiền                     | DECIMAL      | 15,2      | Không rỗng (NOT NULL)                          |
| created_at   | Thời gian tạo                  | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                      |

## Bảng PAYMENT_METHODS (Phương thức thanh toán)

| Tên cột    | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                             |
| ---------- | ------------------------ | ------------ | --------- | ----------------------------------------------------------------------------------- |
| id         | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                                             |
| name       | Tên phương thức          | VARCHAR      | 100       | Không rỗng (NOT NULL)                                                               |
| code       | Mã phương thức           | VARCHAR      | 50        | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                                            |
| type       | Loại phương thức         | VARCHAR      | 20        | Không rỗng (NOT NULL), CHECK (type IN ('cod', 'banking', 'ewallet', 'credit_card')) |
| is_active  | Trạng thái hoạt động     | BOOLEAN      |           | DEFAULT TRUE                                                                        |
| config     | Cấu hình phương thức     | JSONB        |           | Cấu hình API, thông tin ngân hàng, etc.                                             |
| created_at | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                           |
| updated_at | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                           |

## Bảng SHIPPING_METHODS (Phương thức vận chuyển)

| Tên cột            | Giải thích                | Kiểu dữ liệu | Maxlength | Ghi chú                                 |
| ------------------ | ------------------------- | ------------ | --------- | --------------------------------------- |
| id                 | Khóa chính (PRIMARY KEY)  | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid()) |
| name               | Tên phương thức           | VARCHAR      | 100       | Không rỗng (NOT NULL)                   |
| carrier            | Đơn vị vận chuyển         | VARCHAR      | 100       | Không rỗng (NOT NULL)                   |
| description        | Mô tả phương thức         | TEXT         |           |                                         |
| base_fee           | Phí cơ bản                | DECIMAL      | 15,2      | Không rỗng (NOT NULL)                   |
| fee_per_kg         | Phí theo kg               | DECIMAL      | 15,2      | DEFAULT 0                               |
| min_weight         | Trọng lượng tối thiểu     | DECIMAL      | 8,2       | DEFAULT 0                               |
| max_weight         | Trọng lượng tối đa        | DECIMAL      | 8,2       |                                         |
| estimated_days_min | Số ngày dự kiến tối thiểu | INTEGER      |           |                                         |
| estimated_days_max | Số ngày dự kiến tối đa    | INTEGER      |           |                                         |
| is_active          | Trạng thái hoạt động      | BOOLEAN      |           | DEFAULT TRUE                            |
| created_at         | Thời gian tạo             | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP               |
| updated_at         | Thời gian cập nhật        | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP               |

## Bảng ORDER_SHIPPING (Thông tin vận chuyển đơn hàng)

| Tên cột            | Giải thích                  | Kiểu dữ liệu | Maxlength | Ghi chú                                                |
| ------------------ | --------------------------- | ------------ | --------- | ------------------------------------------------------ |
| id                 | Khóa chính (PRIMARY KEY)    | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                |
| order_id           | ID đơn hàng                 | UUID         |           | Không rỗng (NOT NULL), Tham chiếu orders(id)           |
| shipping_method_id | ID phương thức vận chuyển   | UUID         |           | Không rỗng (NOT NULL), Tham chiếu shipping_methods(id) |
| tracking_number    | Mã vận đơn                  | VARCHAR      | 100       |                                                        |
| carrier            | Đơn vị vận chuyển           | VARCHAR      | 100       |                                                        |
| status             | Trạng thái vận chuyển       | VARCHAR      | 50        |                                                        |
| estimated_delivery | Thời gian dự kiến giao hàng | TIMESTAMP    |           |                                                        |
| actual_delivery    | Thời gian thực tế giao hàng | TIMESTAMP    |           |                                                        |
| notes              | Ghi chú                     | TEXT         |           |                                                        |
| created_at         | Thời gian tạo               | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                              |
| updated_at         | Thời gian cập nhật          | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                              |

## Bảng PROMOTIONS (Khuyến mãi)

| Tên cột             | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                                               |
| ------------------- | ------------------------ | ------------ | --------- | ----------------------------------------------------------------------------------------------------- |
| id                  | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                                                               |
| name                | Tên khuyến mãi           | VARCHAR      | 255       | Không rỗng (NOT NULL)                                                                                 |
| code                | Mã khuyến mãi            | VARCHAR      | 50        | Duy nhất (UNIQUE)                                                                                     |
| type                | Loại khuyến mãi          | VARCHAR      | 20        | Không rỗng (NOT NULL), CHECK (type IN ('percentage', 'fixed_amount', 'free_shipping', 'buy_x_get_y')) |
| value               | Giá trị khuyến mãi       | DECIMAL      | 15,2      | Không rỗng (NOT NULL)                                                                                 |
| min_order_amount    | Đơn hàng tối thiểu       | DECIMAL      | 15,2      | DEFAULT 0                                                                                             |
| max_discount_amount | Giảm giá tối đa          | DECIMAL      | 15,2      |                                                                                                       |
| usage_limit         | Giới hạn sử dụng         | INTEGER      |           |                                                                                                       |
| used_count          | Số lần đã sử dụng        | INTEGER      |           | DEFAULT 0                                                                                             |
| start_date          | Ngày bắt đầu             | TIMESTAMP    |           | Không rỗng (NOT NULL)                                                                                 |
| end_date            | Ngày kết thúc            | TIMESTAMP    |           | Không rỗng (NOT NULL)                                                                                 |
| is_active           | Trạng thái hoạt động     | BOOLEAN      |           | DEFAULT TRUE                                                                                          |
| created_at          | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                                             |
| updated_at          | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                                             |

## Bảng PROMOTION_PRODUCTS (Sản phẩm áp dụng khuyến mãi)

| Tên cột      | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                          |
| ------------ | ------------------------ | ------------ | --------- | ------------------------------------------------ |
| id           | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())          |
| promotion_id | ID khuyến mãi            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu promotions(id) |
| product_id   | ID sản phẩm              | UUID         |           | Tham chiếu products(id)                          |
| category_id  | ID danh mục              | UUID         |           | Tham chiếu categories(id)                        |
| brand_id     | ID thương hiệu           | UUID         |           | Tham chiếu brands(id)                            |
| created_at   | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                        |

## Bảng USER_PROMOTIONS (Khuyến mãi của người dùng)

| Tên cột      | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                          |
| ------------ | ------------------------ | ------------ | --------- | ------------------------------------------------ |
| id           | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())          |
| user_id      | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id)      |
| promotion_id | ID khuyến mãi            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu promotions(id) |
| used_at      | Thời gian sử dụng        | TIMESTAMP    |           |                                                  |
| order_id     | ID đơn hàng              | UUID         |           | Tham chiếu orders(id)                            |
| created_at   | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                        |

## Bảng REVIEWS (Đánh giá sản phẩm)

| Tên cột       | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                    |
| ------------- | ------------------------ | ------------ | --------- | ---------------------------------------------------------- |
| id            | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                    |
| user_id       | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id)                |
| product_id    | ID sản phẩm              | UUID         |           | Không rỗng (NOT NULL), Tham chiếu products(id)             |
| order_id      | ID đơn hàng              | UUID         |           | Tham chiếu orders(id)                                      |
| rating        | Điểm đánh giá            | INTEGER      |           | Không rỗng (NOT NULL), CHECK (rating >= 1 AND rating <= 5) |
| title         | Tiêu đề đánh giá         | VARCHAR      | 255       |                                                            |
| content       | Nội dung đánh giá        | TEXT         |           |                                                            |
| images        | Hình ảnh đánh giá        | TEXT[]       |           | Mảng URLs của hình ảnh đánh giá                            |
| is_verified   | Đã xác thực              | BOOLEAN      |           | DEFAULT FALSE                                              |
| is_approved   | Đã duyệt                 | BOOLEAN      |           | DEFAULT TRUE                                               |
| helpful_count | Số lượt hữu ích          | INTEGER      |           | DEFAULT 0                                                  |
| created_at    | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                  |
| updated_at    | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                  |

## Bảng REVIEW_RESPONSES (Phản hồi đánh giá)

| Tên cột           | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                       |
| ----------------- | ------------------------ | ------------ | --------- | --------------------------------------------- |
| id                | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())       |
| review_id         | ID đánh giá              | UUID         |           | Không rỗng (NOT NULL), Tham chiếu reviews(id) |
| user_id           | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id)   |
| content           | Nội dung phản hồi        | TEXT         |           | Không rỗng (NOT NULL)                         |
| is_admin_response | Phản hồi từ admin        | BOOLEAN      |           | DEFAULT FALSE                                 |
| created_at        | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                     |

## Bảng REVIEW_LIKES (Thích đánh giá)

| Tên cột    | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                       |
| ---------- | ------------------------ | ------------ | --------- | --------------------------------------------- |
| id         | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())       |
| review_id  | ID đánh giá              | UUID         |           | Không rỗng (NOT NULL), Tham chiếu reviews(id) |
| user_id    | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id)   |
| created_at | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                     |

## Bảng SUPPORT_TICKETS (Phiếu hỗ trợ)

| Tên cột       | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                                   |
| ------------- | ------------------------ | ------------ | --------- | ----------------------------------------------------------------------------------------- |
| id            | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                                                   |
| ticket_number | Số phiếu hỗ trợ          | VARCHAR      | 50        | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                                                  |
| user_id       | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id)                                               |
| subject       | Tiêu đề phiếu            | VARCHAR      | 255       | Không rỗng (NOT NULL)                                                                     |
| description   | Mô tả vấn đề             | TEXT         |           | Không rỗng (NOT NULL)                                                                     |
| category      | Danh mục vấn đề          | VARCHAR      | 50        | Không rỗng (NOT NULL)                                                                     |
| priority      | Độ ưu tiên               | VARCHAR      | 20        | NOT NULL, DEFAULT 'medium', CHECK (priority IN ('low', 'medium', 'high', 'urgent'))       |
| status        | Trạng thái phiếu         | VARCHAR      | 20        | NOT NULL, DEFAULT 'open', CHECK (status IN ('open', 'in_progress', 'resolved', 'closed')) |
| assigned_to   | Người được phân công     | UUID         |           | Tham chiếu users(id)                                                                      |
| resolution    | Giải pháp                | TEXT         |           |                                                                                           |
| created_at    | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                                 |
| updated_at    | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                                 |
| resolved_at   | Thời gian giải quyết     | TIMESTAMP    |           |                                                                                           |
| closed_at     | Thời gian đóng           | TIMESTAMP    |           |                                                                                           |

## Bảng SUPPORT_MESSAGES (Tin nhắn hỗ trợ)

| Tên cột          | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                               |
| ---------------- | ------------------------ | ------------ | --------- | ----------------------------------------------------- |
| id               | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())               |
| ticket_id        | ID phiếu hỗ trợ          | UUID         |           | Không rỗng (NOT NULL), Tham chiếu support_tickets(id) |
| user_id          | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id)           |
| content          | Nội dung tin nhắn        | TEXT         |           | Không rỗng (NOT NULL)                                 |
| is_admin_message | Tin nhắn từ admin        | BOOLEAN      |           | DEFAULT FALSE                                         |
| attachments      | Tệp đính kèm             | TEXT[]       |           | Mảng URLs của tệp đính kèm                            |
| created_at       | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                             |

## Bảng COMPLAINTS (Khiếu nại)

| Tên cột          | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                                |
| ---------------- | ------------------------ | ------------ | --------- | -------------------------------------------------------------------------------------- |
| id               | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                                                |
| complaint_number | Số khiếu nại             | VARCHAR      | 50        | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                                               |
| user_id          | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id)                                            |
| order_id         | ID đơn hàng              | UUID         |           | Tham chiếu orders(id)                                                                  |
| subject          | Tiêu đề khiếu nại        | VARCHAR      | 255       | Không rỗng (NOT NULL)                                                                  |
| description      | Mô tả khiếu nại          | TEXT         |           | Không rỗng (NOT NULL)                                                                  |
| category         | Danh mục khiếu nại       | VARCHAR      | 50        | Không rỗng (NOT NULL)                                                                  |
| priority         | Độ ưu tiên               | VARCHAR      | 20        | NOT NULL, DEFAULT 'medium', CHECK (priority IN ('low', 'medium', 'high', 'urgent'))    |
| status           | Trạng thái khiếu nại     | VARCHAR      | 20        | NOT NULL, DEFAULT 'new', CHECK (status IN ('new', 'processing', 'resolved', 'closed')) |
| assigned_to      | Người được phân công     | UUID         |           | Tham chiếu users(id)                                                                   |
| resolution       | Giải pháp                | TEXT         |           |                                                                                        |
| compensation     | Đền bù                   | TEXT         |           |                                                                                        |
| created_at       | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                              |
| updated_at       | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                              |
| resolved_at      | Thời gian giải quyết     | TIMESTAMP    |           |                                                                                        |
| closed_at        | Thời gian đóng           | TIMESTAMP    |           |                                                                                        |

## Bảng PRE_ORDERS (Đặt trước)

| Tên cột           | Giải thích                  | Kiểu dữ liệu | Maxlength | Ghi chú                                                                                                                             |
| ----------------- | --------------------------- | ------------ | --------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| id                | Khóa chính (PRIMARY KEY)    | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                                                                                             |
| pre_order_number  | Số đặt trước                | VARCHAR      | 50        | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                                                                                            |
| user_id           | ID người dùng               | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id)                                                                                         |
| product_id        | ID sản phẩm                 | UUID         |           | Không rỗng (NOT NULL), Tham chiếu products(id)                                                                                      |
| quantity          | Số lượng                    | INTEGER      |           | Không rỗng (NOT NULL)                                                                                                               |
| price             | Giá đặt trước               | DECIMAL      | 15,2      | Không rỗng (NOT NULL)                                                                                                               |
| status            | Trạng thái đặt trước        | VARCHAR      | 20        | NOT NULL, DEFAULT 'pending', CHECK (status IN ('pending', 'confirmed', 'processing', 'ready', 'shipped', 'delivered', 'cancelled')) |
| deposit_amount    | Số tiền cọc                 | DECIMAL      | 15,2      | DEFAULT 0                                                                                                                           |
| remaining_amount  | Số tiền còn lại             | DECIMAL      | 15,2      |                                                                                                                                     |
| expected_delivery | Thời gian dự kiến giao hàng | TIMESTAMP    |           |                                                                                                                                     |
| actual_delivery   | Thời gian thực tế giao hàng | TIMESTAMP    |           |                                                                                                                                     |
| notes             | Ghi chú                     | TEXT         |           |                                                                                                                                     |
| created_at        | Thời gian tạo               | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                                                                           |
| updated_at        | Thời gian cập nhật          | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                                                                           |

## Bảng SPECIAL_REQUESTS (Yêu cầu đặc biệt)

| Tên cột        | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                                                                |
| -------------- | ------------------------ | ------------ | --------- | ---------------------------------------------------------------------------------------------------------------------- |
| id             | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                                                                                |
| request_number | Số yêu cầu               | VARCHAR      | 50        | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                                                                               |
| user_id        | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id)                                                                            |
| product_name   | Tên sản phẩm yêu cầu     | VARCHAR      | 255       | Không rỗng (NOT NULL)                                                                                                  |
| brand          | Thương hiệu              | VARCHAR      | 100       |                                                                                                                        |
| series         | Tên series               | VARCHAR      | 100       |                                                                                                                        |
| scale          | Tỷ lệ mô hình            | VARCHAR      | 50        |                                                                                                                        |
| description    | Mô tả yêu cầu            | TEXT         |           | Không rỗng (NOT NULL)                                                                                                  |
| budget_min     | Ngân sách tối thiểu      | DECIMAL      | 15,2      |                                                                                                                        |
| budget_max     | Ngân sách tối đa         | DECIMAL      | 15,2      |                                                                                                                        |
| status         | Trạng thái yêu cầu       | VARCHAR      | 20        | NOT NULL, DEFAULT 'pending', CHECK (status IN ('pending', 'reviewing', 'quoted', 'accepted', 'rejected', 'completed')) |
| admin_response | Phản hồi từ admin        | TEXT         |           |                                                                                                                        |
| quoted_price   | Giá báo giá              | DECIMAL      | 15,2      |                                                                                                                        |
| created_at     | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                                                              |
| updated_at     | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                                                              |

## Bảng POSTS (Bài viết)

| Tên cột        | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                                         |
| -------------- | ------------------------ | ------------ | --------- | ------------------------------------------------------------------------------- |
| id             | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                                         |
| title          | Tiêu đề bài viết         | VARCHAR      | 255       | Không rỗng (NOT NULL)                                                           |
| slug           | URL slug                 | VARCHAR      | 255       | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                                        |
| content        | Nội dung bài viết        | TEXT         |           | Không rỗng (NOT NULL)                                                           |
| excerpt        | Tóm tắt bài viết         | TEXT         |           |                                                                                 |
| featured_image | Hình ảnh nổi bật         | TEXT         |           |                                                                                 |
| author_id      | ID tác giả               | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id)                                     |
| status         | Trạng thái bài viết      | VARCHAR      | 20        | NOT NULL, DEFAULT 'draft', CHECK (status IN ('draft', 'published', 'archived')) |
| post_type      | Loại bài viết            | VARCHAR      | 20        | DEFAULT 'post', CHECK (post_type IN ('post', 'page', 'announcement'))           |
| view_count     | Số lượt xem              | INTEGER      |           | DEFAULT 0                                                                       |
| like_count     | Số lượt thích            | INTEGER      |           | DEFAULT 0                                                                       |
| comment_count  | Số lượt bình luận        | INTEGER      |           | DEFAULT 0                                                                       |
| is_featured    | Bài viết nổi bật         | BOOLEAN      |           | DEFAULT FALSE                                                                   |
| published_at   | Thời gian xuất bản       | TIMESTAMP    |           |                                                                                 |
| created_at     | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                       |
| updated_at     | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                                       |

## Bảng POST_COMMENTS (Bình luận bài viết)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                     |
| ----------- | ------------------------ | ------------ | --------- | ------------------------------------------- |
| id          | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())     |
| post_id     | ID bài viết              | UUID         |           | Không rỗng (NOT NULL), Tham chiếu posts(id) |
| user_id     | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id) |
| parent_id   | ID bình luận cha         | UUID         |           | Tham chiếu post_comments(id)                |
| content     | Nội dung bình luận       | TEXT         |           | Không rỗng (NOT NULL)                       |
| is_approved | Đã duyệt                 | BOOLEAN      |           | DEFAULT TRUE                                |
| like_count  | Số lượt thích            | INTEGER      |           | DEFAULT 0                                   |
| created_at  | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                   |
| updated_at  | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                   |

## Bảng NOTIFICATIONS (Thông báo)

| Tên cột    | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                     |
| ---------- | ------------------------ | ------------ | --------- | ------------------------------------------- |
| id         | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())     |
| user_id    | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id) |
| title      | Tiêu đề thông báo        | VARCHAR      | 255       | Không rỗng (NOT NULL)                       |
| content    | Nội dung thông báo       | TEXT         |           | Không rỗng (NOT NULL)                       |
| type       | Loại thông báo           | VARCHAR      | 50        | Không rỗng (NOT NULL)                       |
| data       | Dữ liệu bổ sung          | JSONB        |           | Dữ liệu bổ sung cho thông báo               |
| is_read    | Đã đọc                   | BOOLEAN      |           | DEFAULT FALSE                               |
| read_at    | Thời gian đọc            | TIMESTAMP    |           |                                             |
| created_at | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                   |

## Bảng WISHLISTS (Danh sách yêu thích)

| Tên cột    | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                        |
| ---------- | ------------------------ | ------------ | --------- | ---------------------------------------------- |
| id         | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())        |
| user_id    | ID người dùng            | UUID         |           | Không rỗng (NOT NULL), Tham chiếu users(id)    |
| product_id | ID sản phẩm              | UUID         |           | Không rỗng (NOT NULL), Tham chiếu products(id) |
| created_at | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                      |

## Bảng SYSTEM_SETTINGS (Cài đặt hệ thống)

| Tên cột     | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                                           |
| ----------- | ------------------------ | ------------ | --------- | ----------------------------------------------------------------- |
| id          | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid())                           |
| key         | Khóa cài đặt             | VARCHAR      | 100       | Duy nhất (UNIQUE), Không rỗng (NOT NULL)                          |
| value       | Giá trị cài đặt          | TEXT         |           |                                                                   |
| type        | Loại dữ liệu             | VARCHAR      | 20        | NOT NULL, CHECK (type IN ('string', 'number', 'boolean', 'json')) |
| description | Mô tả cài đặt            | TEXT         |           |                                                                   |
| category    | Danh mục cài đặt         | VARCHAR      | 50        |                                                                   |
| is_public   | Cài đặt công khai        | BOOLEAN      |           | DEFAULT FALSE                                                     |
| created_at  | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                         |
| updated_at  | Thời gian cập nhật       | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP                                         |

## Bảng AUDIT_LOGS (Nhật ký kiểm toán)

| Tên cột    | Giải thích               | Kiểu dữ liệu | Maxlength | Ghi chú                                 |
| ---------- | ------------------------ | ------------ | --------- | --------------------------------------- |
| id         | Khóa chính (PRIMARY KEY) | UUID         |           | Tự động tạo (DEFAULT gen_random_uuid()) |
| user_id    | ID người dùng            | UUID         |           | Tham chiếu users(id)                    |
| action     | Hành động                | VARCHAR      | 100       | Không rỗng (NOT NULL)                   |
| table_name | Tên bảng                 | VARCHAR      | 100       | Không rỗng (NOT NULL)                   |
| record_id  | ID bản ghi               | UUID         |           | Không rỗng (NOT NULL)                   |
| old_values | Giá trị cũ               | JSONB        |           |                                         |
| new_values | Giá trị mới              | JSONB        |           |                                         |
| ip_address | Địa chỉ IP               | INET         |           |                                         |
| user_agent | Thông tin trình duyệt    | TEXT         |           |                                         |
| created_at | Thời gian tạo            | TIMESTAMP    |           | DEFAULT CURRENT_TIMESTAMP               |

---

## GHI CHÚ QUAN TRỌNG

### 1. Quy tắc đặt tên

- Tất cả tên bảng và cột sử dụng chữ thường với dấu gạch dưới
- Tên bảng ở dạng số nhiều (users, products, orders...)
- Tên cột mô tả rõ ràng chức năng

### 2. Kiểu dữ liệu

- **UUID**: Sử dụng cho tất cả khóa chính để tránh xung đột khi scale
- **VARCHAR**: Cho chuỗi có độ dài cố định hoặc giới hạn
- **TEXT**: Cho nội dung dài không giới hạn
- **DECIMAL**: Cho số tiền với độ chính xác cao
- **JSONB**: Cho dữ liệu linh hoạt, có thể query được
- **TIMESTAMP**: Cho thời gian với timezone
- **BOOLEAN**: Cho giá trị true/false

### 3. Ràng buộc (Constraints)

- **PRIMARY KEY**: Khóa chính duy nhất
- **UNIQUE**: Giá trị duy nhất trong bảng
- **NOT NULL**: Không được để trống
- **CHECK**: Kiểm tra giá trị hợp lệ
- **FOREIGN KEY**: Tham chiếu đến bảng khác

### 4. Mối quan hệ

- **1-n**: Một người dùng có nhiều đơn hàng
- **n-n**: Nhiều sản phẩm có thể thuộc nhiều khuyến mãi
- **1-1**: Một đơn hàng có một thông tin vận chuyển

### 5. Indexes được khuyến nghị

- Index trên các cột thường xuyên query (email, status, created_at)
- Composite index cho các query phức tạp
- Full-text search index cho tìm kiếm nội dung
