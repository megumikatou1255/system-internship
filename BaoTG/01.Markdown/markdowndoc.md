# Hướng Dẫn Cơ Bản về Markdown

# Mục Lục

## Giới thiệu về ngôn ngữ Markdown

## Những định dạng phổ biến khi sử dụng Markdown
### 1. Tiêu đề
### 2. Định dang văn bản
### 3. Danh sách
### 4. Tiêu đề và hình ảnh
### 5. Trích dẫn
### 6. Tạo bảng
### 7. Đoạn văn và ngắt dòng
## Kết Luận

## Giới thiệu về ngôn ngữ Markdown

Markdown là một ngôn ngữ đánh dấu nhẹ, được thiết kế để dễ đọc và dễ viết. Nó thường được sử dụng để định dạng văn bản trong tài liệu, README, blog, ghi chú, và trên các nền tảng như GitHub, Reddit, v.v.

---

## Những định dạng phổ biến khi sử dụng Markdown

### 1. Tiêu đề

Dùng dấu `#` để tạo tiêu đề:

```markdown
MARK DOWN

# Tiêu đề cấp 1

## Tiêu đề cấp 2

### Tiêu đề cấp 3

#### Tiêu đề cấp 4

##### Tiêu đề cấp 5

###### Tiêu đề cấp 6
```

OUTPUT:

# Tiêu đề cấp 1

## Tiêu đề cấp 2

### Tiêu đề cấp 3

#### Tiêu đề cấp 4

##### Tiêu đề cấp 5

###### Tiêu đề cấp 6

---

### 2. Định dạng văn bản

Cũng giống như html thì mark down cũng có các thẻ dùng để định dạng cho văn bản

```markdown
MARK DOWN
**Đậm** → **Đậm**  
_Nghiêng_ → _Nghiêng_  
~~Gạch bỏ~~ → ~~Gạch bỏ~~  
`Mã inline` → `Mã inline`
```

OUTPUT:

**Đậm** → **Đậm**  
_Nghiêng_ → _Nghiêng_  
~~Gạch bỏ~~ → ~~Gạch bỏ~~  
`Mã inline` → `Mã inline`

---

### 3. Danh sách

Giống ở html có các thẻ -ul,-ol thì trong mark down cũng có các thẻ để liệt kê danh sách các phần tử đó là:

- Dùng dấu - (gạch ngang), \* (dấu sao) hoặc + (dấu cộng) để tạo danh sách không thứ tự.

```markdown
MARK DOWN

- Mục 1
- Mục 2
- Mục 3
```

OUTPUT:

- Mục 1
- Mục 2
- Mục 3

---

- Dùng số kèm dấu chấm để liệt kê có danh sách

```markdown
MARK DOWN

1. Mục 1
2. Mục 2
3. Mục 3
```

OUTPUT:

1. Mục 1
2. Mục 2
3. Mục 3

---

- Dùng thụt 2,4 khoảng từ đầu dòng để lồng danh sách với nhau

```markdown
MARK DOWN

- Mục 1
  - Mục con 1
  - Mục con 2
- Mục 2
```

OUTPUT:

- Mục 1
  - Mục con 1
  - Mục con 2
- Mục 2

---

### 4.Tiêu đề và hình ảnh

Để trích xuất tiêu đề và hình ảnh ta xài các cấu trúc sau:

```markdown
MARK DOWN
[OpenAI](https://openai.com)

![Logo](https://upload.wikimedia.org/wikipedia/commons/4/4a/Logo_2013_Google.png)
```

OUTPUT:
[OpenAI](https://openai.com)

![Logo](https://upload.wikimedia.org/wikipedia/commons/4/4a/Logo_2013_Google.png)

### 5. Trích dẫn

Có 2 dạng trích dẫn :

- Trích dẫn lồng nhau, ta xài dấu'>'

- Trích dẫn thường ,ta xài dấu '>>'

### 6. Tạo bảng

Để tạo bảng ta có thể lấy qua ví dụ sau:
Tạo 1 bảng về điểm số 3 môn Toán, Lý, Hoá, Trung bình môn và xếp loại

```markdown
MARK DOWN
| Họ và tên | Toán | Lý | Hóa | Trung bình | Xếp loại |
|------------------|------|-----|-----|-------------|------------|
| Nguyễn Văn A | 9.0 | 8.5 | 9.5 | 9.0 | Giỏi |
| Trần Thị B | 7.0 | 6.5 | 8.0 | 7.2 | Khá |
| Lê Văn C | 5.5 | 6.0 | 5.0 | 5.5 | Trung bình |
| Phạm Thị D | 9.5 | 9.0 | 9.0 | 9.2 | Giỏi |
```

OUTPUT:
| Họ và tên | Toán | Lý | Hóa | Trung bình | Xếp loại |
|------------------|------|-----|-----|-------------|------------|
| Nguyễn Văn A | 9.0 | 8.5 | 9.5 | 9.0 | Giỏi |
| Trần Thị B | 7.0 | 6.5 | 8.0 | 7.2 | Khá |
| Lê Văn C | 5.5 | 6.0 | 5.0 | 5.5 | Trung bình |
| Phạm Thị D | 9.5 | 9.0 | 9.0 | 9.2 | Giỏi |

---
### 7. Đoạn văn và ngắt dòng
Đoạn văn cách nhau bởi 1 dòng trắng
Xuống dòng kết thúc bằng 2 khoảng cách trắng hoặc bằng thẻ 
```markdown
'<br>'
```
---
## Kết Luận
Markdown là một công cụ đơn giản nhưng mạnh mẽ, hỗ trợ rất tốt trong việc viết tài liệu, ghi chú và giao tiếp kỹ thuật. Dù còn một số hạn chế, nhưng Markdown đang ngày càng phổ biến trong nhiều lĩnh vực từ kỹ thuật đến giáo dục.

Tài liệu tham khảo:

https://daringfireball.net/projects/markdown/

https://commonmark.org/

https://guides.github.com/features/mastering-markdown/
