project-g3
==========

Project cuối kỳ 1 của nhóm 3

Project có sử dụng một số công nghệ sau:
- Jekyll - template engine
- Bootstrap - framework lập trình giao diện web

Jekyll
======

[Jekyll](https://github.com/mojombo/Jekyll) là một hệ thống tạo site dựa theo template. Lập trình viên tạo
các template trong thư mục `_layouts` (ví dụ như default.html)

    <head>
    </head>
    <body>
        {{ content }}
    </body>

Sau đó tạo các
trang bất kỳ khởi đầu bằng một đoạn mã [YAML Front Matter](https://github.com/mojombo/Jekyll/wiki/yaml-front-matter) như thế này:

    ---
    layout: default
    title: Homepage
    description: It's really is a homepage.
    ---
    
    nội dung
    
dòng đầu tiên (`layout: default`) để thông báo cho Jekyll biết là file này sẽ
sử dụng template có tên là _default_. Dòng thứ 2 và 3 self-explanatory. Toàn bộ
nội dung file này tương ứng với biến `{{ content }}` trong file template và sẽ
được thay thế vào vị trí của biến `{{ content }}`.

Khi chạy lệnh `jekyll --server --auto` thì Jekyll sẽ convert tất cả các trang
vừa tạo vào trong thư mục `_site` và tạo một webserver ở địa chỉ `0.0.0.0:4000`.

Ngoài ra, tất cả các file trong thư mục _posts có dạng `năm-tháng-ngày-tên-post.md` đều
được convert tự động thành các bài viết như một blog `_site/năm/tháng/ngày/tên-post.html`

Project sử dụng tính năng Pages của Github để host site. Github Pages sử dụng
Jekyll làm backend nên chỉ cần push một commit lên nhánh gh-pages là Github sẽ
tự động build trang web mới tại địa chỉ `http://<tên người dùng>.github.com/<tên project>`.

Ngôn ngữ tạo template của Jekyll là liquid. Trong một trang template, chúng ta
có thể sử dụng các biến và cấu trúc điều khiển của liquid. VD:

    <head>
        <title>{{ page.title }}</title>
        {% unless page.description == null %}
        <meta name="description" content="{{ page.description }}">
        {% endunless %}
    </head>
    <body>
        <h1>Recent posts:</h1>
        {% for post in site.posts limit:10 %}
        <h2>{{ post.title }}</h2>
        <p>{{ post.description }}</p>
        {% unless post.tags == empty %}
        <p>Tags: 
        {% for tag in post.tags %}
            {{ tag }} | 
        {% endfor %}
        </p>
        {% endfor %}
    </body>
    
Hướng dẫn chi tiết hơn về Jekyll có thể được tìm thấy ở [trang chủ](https://github.com/mojombo/Jekyll).
Các biến liquid có thể tìm hiểu tại [đây](https://github.com/mojombo/Jekyll/wiki/template-data).
Jekyll còn có một số [extension cho liquid](https://github.com/mojombo/Jekyll/wiki/liquid-extensions)
giúp đỡ nhiều cho việc tạo template.

Bootstrap
========

[Bootstrap](http://twitter.github.com/bootstrap/) là một tập hợp các file css, js
và hình ảnh được thiết kế sẵn để giúp tăng tốc quá trình build giao diện cho một
website. Nhiều vấn đề khó như tạo layout bằng grid, animation, widget, responsive
design đã được Bootstrap thiết kế trước nên giảm bớt gánh nặng cho lập trình viên
một cách đáng kể.

Hướng dẫn sử dụng Bootstrap có thể tìm hiểu tại [đây](http://twitter.github.com/bootstrap/getting-started.html)
