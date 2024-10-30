# Shop-app-backend
Developed a backend e-commerce shop application using Spring Boot

## API specification
### 1. User
#### 1.1. Register
- **URL**: `/api/user/register`
- **Method**: `POST`
- **Request Body**:
```json
{
  "full_name": "John Doe",
  "phone_number": "0962898984",
  "address": "123 Main Street, City, Country",
  "password": "strongpassword123",
  "retyped_password": "strongpassword123",
  "date_of_birth": "1990-01-01",
  "role_id": 1
}

```
- **Response**:
```json
{
  "message": "Register successfully",
  "user": {
    "createdAt": [
      2024,
      10,
      30,
      12,
      13,
      38,
      910623400
    ],
    "updatedAt": [
      2024,
      10,
      30,
      12,
      13,
      38,
      910623400
    ],
    "id": 11,
    "fullName": "John Doe",
    "phoneNumber": "0962898984",
    "address": "123 Main Street, City, Country",
    "password": "$2a$10$ZOwh4rpEJiP7Y6PRN8oV9OCgbX6CUiGiCthf1GsRF6ITWX68TKX/G",
    "active": true,
    "dateOfBirth": 631152000000,
    "facebookAccountId": 0,
    "googleAccountId": 0,
    "role": {
      "id": 1,
      "name": "user"
    },
    "enabled": true,
    "credentialsNonExpired": true,
    "accountNonExpired": true,
    "accountNonLocked": true,
    "username": "0962898984",
    "authorities": [
      {
        "authority": "ROLE_USER"
      }
    ]
  }
}
```

#### 1.2. Login
- **URL**: `/api/user/login`
- **Method**: `POST`
- **Request Body**:
```json
{
  "phone_number": "0962898984",
  "password": "strongpassword123"
}

```
- **Response**:
```json
{
  "message": "Login successfully",
  "token": "eyJhbGciOiJIUzI1NiJ9.eyJwaG9uZU51bWJlciI6IjA5NjI4OTg5ODQiLCJ1c2VySWQiOjExLCJzdWIiOiIwOTYyODk4OTg0IiwiZXhwIjoxNzMyODU3MzY4fQ.WVFUkjwLWFi7OdHZaGwl9N5LXCvAaeFVNz4k8kbgoCM"
}
```

#### 1.3. Get User Details
- **URL**: `/api/user/details/{user_id}`
- **Method**: `GET`
- **Role**: `user`
- **Response**:
```json
{
  "user": {
    "id": 11,
    "fullName": "John Doe",
    "phoneNumber": "0962898984",
    "address": "123 Main Street, City, Country",
    "dateOfBirth": "1990-01-01",
    "role": {
      "id": 1,
      "name": "user"
    }
  }
}
```
### 2. Product

#### 2.1. Create Product
- **URL**: `/api/products`
- **Method**: `POST`
- **Role**: `admin`
- **Request Body**:
```json
{
  "name": "MacBook Air 15 inch 2023",
  "price": 812.34,
  "description": "This is a test product",
  "category_id": 2
}
```
- **Response**:
```json
{
  "message": "Product created successfully",
  "product": {
    "id": 1,
    "name": "MacBook Air 15 inch 2023",
    "price": 812.34,
    "description": "This is a test product",
    "category": {
      "id": 2,
      "name": "Laptop"
    }
  }
}
```
#### 2.2. Get Product List
- **URL**: `/api/products`
- **Method**: `GET`
- **Query Params**:
    - `page`: page number for pagination
    - `limit`: maximum number of products per page
    - `keyword`: search keyword
    - `category_id`: filter by category
- **Response**:
```json
{
  "products": [
    {
      "id": 1,
      "name": "MacBook Air 15 inch 2023",
      "price": 812.34,
      "category": {
        "id": 2,
        "name": "Electronics"
      }
    },
    {
      "id": 2,
      "name": "iPad Pro 2023",
      "price": 999.99,
      "category": {
        "id": 2,
        "name": "Electronics"
      }
    }
  ],
  "page": 1,
  "totalPages": 5
}
```
#### 2.3. Get Product Details
- **URL**: `/api/products/{product_id}`
- **Method**: `GET`
- **Response**:
```json
{
  "product": {
    "id": 1,
    "name": "MacBook Air 15 inch 2023",
    "price": 812.34,
    "description": "This is a test product",
    "category": {
      "id": 2,
      "name": "Laptop"
    }
  }
}
```

### 3. Order

#### 3.1. Create Order
- **URL**: `/api/orders`
- **Method**: `POST`
- **Role**: `user`
- **Request Body**:
```json
{
  "user_id": 5,
  "fullname": "Nguyễn Văn X",
  "email": "nvxx@yahoo.com",
  "phone_number": "123456789",
  "address": "Nhà A, ngõ B, quận C, thành phố D",
  "note": "Hàng dễ vỡ xin nhẹ tay",
  "total_money": 123.45,
  "shipping_method": "express",
  "payment_method": "cod",
  "cart_items": [
    {
      "product_id": 5,
      "quantity": 2
    },
    {
      "product_id": 7,
      "quantity": 1
    }
  ]
}
  ```
- **Response**:
```json
{
  "message": "Order created successfully",
  "order": {
    "id": 15,
    "userId": 5,
    "fullname": "Nguyễn Văn X",
    "totalMoney": 123.45,
    "status": "pending",
    "createdAt": "2024-10-30T12:15:30Z"
  }
}
  ```
#### 3.2. Get Order
- **URL**: `/api/orders/{order_id}`
- **Method**: `GET`
- **Role**: `user, admin`
- **Response**:
```json
{
  "order": {
    "id": 15,
    "userId": 5,
    "fullname": "Nguyễn Văn X",
    "email": "nvxx@yahoo.com",
    "phone_number": "123456789",
    "address": "Nhà A, ngõ B, quận C, thành phố D",
    "note": "Hàng dễ vỡ xin nhẹ tay",
    "totalMoney": 123.45,
    "status": "pending",
    "createdAt": "2024-10-30T12:15:30Z",
    "cartItems": [
      {
        "productId": 5,
        "quantity": 2,
        "price": 60.00
      },
      {
        "productId": 7,
        "quantity": 1,
        "price": 45.00
      }
    ]
  }
}
```

### 4. Order Detail
#### 4.1. Add Order Detail
- **URL**: `/api/order_details`
- **Method**: `POST`
- **Request Body**:
```json
{
  "order_id": 15,
  "product_id": 5,
  "price": 60.00,
  "quantity": 2,
  "total_money": 120.00,
  "color": "#ff00ff"
}
  ```
- **Response**:
```json
{
  "message": "Order detail created successfully",
  "orderDetail": {
    "id": 1,
    "orderId": 15,
    "productId": 5,
    "price": 60.00,
    "quantity": 2,
    "totalMoney": 120.00,
    "color": "#ff00ff"
  }
}
  ```
#### 4.2. Get Order Detail
- **URL**: `/api/order_details/{order_detail_id}`
- **Method**: `GET`
- **Response**:
```json
{
  "orderDetail": {
    "id": 101,
    "orderId": 15,
    "productId": 5,
    "price": 60.00,
    "quantity": 2,
    "totalMoney": 120.00,
    "color": "#ff00ff"
  }
}
```
