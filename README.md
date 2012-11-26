project-g3
==========

Project cuối kỳ 1 của nhóm 3

Project có sử dụng một số công nghệ sau:

- [Git](#git) - Quản lý phiên bản cho mã nguồn
- [Jekyll](#jekyll) - template engine
- [Bootstrap](#bootstrap) - framework lập trình giao diện web
- [HTML5 Boilerplate](https://github.com/h5bp/html5-boilerplate) - một tập hợp những guideline và code mẫu để đảm bảo
code HTML5 có thể chạy tốt nhất trên nhiều browser khác nhau.

<h2 id="git">Git</h2>
Git là phần mềm quản lý mã nguồn phân tán.

### Basics

Để làm việc nhóm cơ bản với git thì cần hiểu một số thuật ngữ sau:

- `repository` : một thư mục chứa code và được quản lý bởi git
- `commit` (danh từ) : một phiên bản của repo
- `commit` (động từ) : ghi chép những thay đổi và tạo một phiên bản mới
- `branch` : (nhánh) một tập hợp những commit theo trật tự thời gian. Các nhánh
có thể được tạo ra từ cùng một commit và đi theo các hướng phát triển khác nhau.
- `stage` (động từ) : lên danh sách những file đã thay đổi để chuẩn bị commit

và một số lệnh sau:

- `git checkout <tên nhánh hoặc mã hash của commit>` : chuyển thư mục hiện tại
về một commit trong quá khứ hoặc một nhánh khác
- `git checkout -b <tên nhánh>` : tạo một nhánh mới và checkout sang nhánh đó
- `git branch` : hiện danh sách tất cả các branch
- `git branch <tên nhánh>` : tạo một nhánh mới
- `git pull` : lấy tất cả các cập nhật mới nhất từ server về
- `git push` : đưa những thay đổi ở máy hiện tại lên server
- `git merge <tên nhánh hoặc mã hash của commit>` : ghép những thay đổi ở nhánh
(hoặc commit) này sang nhánh hiện tại
- `git add <đường dẫn đến file>` : cho các file này vào diện chuẩn bị commit (staging)
- `git commit [-a] [-m "<Tóm tắt nội dung commit>"]` : Commit những thay đổi đã
tạo trong nhánh hiện tại. Thêm `-a` để tự động stage tất cả các file đã thay đổi.
Thêm `-m "<tóm tắt>"` để ghi commit message trực tiếp mà không phải vào giao diện
vim (default trên Windows, khó sử dụng với người mới).

  _NOTE_ Trong Vim, nhấn `i` để vào chế độ edit, nhấn `Escape :wq Enter` để ghi file và
quit.
- `git stash` : ghi tất cả các thay đổi chưa commit vào vùng nhớ tạm (stash). Sau
lệnh này hiện trạng của repo là clean.
- `git stash pop` : apply các thay đổi trong stash vào nhánh hiện tại nhưng chưa
commit. Hai lệnh này thường dùng để hỗ trợ di chuyển qua lại giữa các nhánh mà không cần
commit những công việc đang dang dở.

Ngoài ra còn có một số lệnh mà có thể dùng giao diện đồ họa để thay thế thì tiện hơn
(gitk, Github 4 Windows, GitTortoise, ...):

- `git status` : xem hiện trạng của repo hiện tại (có file nào chưa commit, file nào
đã thuộc diện staging,...)
- `git diff` : so sánh hiện trạng của thư mục hiện tại với commit gần đây nhất
- `git whatchanged` : hiện lịch sử commit của nhánh hiện tại

### Workflow:
1. Clone repository của nhóm (chỉ cần làm một lần):
    
    `git clone https://github.com/lewtds/project-g3.git`
    
2. Xem xét việc cần làm, đặt một cái tên gợi nhớ cho công việc đó (trong ví dụ này giả định là `fix-footer`)
sau đó tạo một branch mới dựa trên branch gh-pages với tên đó:

    `git checkout -b fix-footer`
    
3. Sửa code, viết code, test code và commit trên branch vừa tạo
4. Khi cảm thấy ổn oy thì chuẩn bị push lên server:
  - Tải các thay đổi mới nhất của mọi người trên server:
        
        `git pull`      
  - Checkout branch gh-pages và merge những thay đổi vừa tạo:
  
            git checkout gh-pages
            git merge fix-footer
  - Nếu có conflict thì resolve và commit
  - Push lên server:
  
        `git push`
5. Quay lại bước 2

### Cách resolve conflict:
Conflict xảy ra khi 2 người (hoặc một người nhưng ở 2 nhánh) cùng chỉnh sửa một
phần của một file. VD:

    (file gốc)
    Trăm năm trong cõi người ta
    Chữ tài chữ mệnh khéo là ghét nhau

    (nhánh a)
    Trăm năm trong cõi người ta
    Chữ tài chữ mệnh khéo là thích nhau
    
    (nhánh b)
    Trăm năm trong cõi người ta
    Chữ sinh chữ mệnh khéo là ghét nhau
    
Khi merge nhánh a vào nhánh b (hoặc ngược lại) thì sẽ xảy ra conflict với message
kiểu như thế này:

    Auto-merging <tên nhánh>
    CONFLICT (content): Merge conflict in <tên file conflict>
    Automatic merge failed; fix conflicts and then commit the result.
    
Conflict
sẽ tạo ra tình huống dở dang chưa commit cho repo. Trong file conflict sẽ hiện
ra đoạn so sánh để giúp lập trình viên giải quyết conflict:

    Trăm năm trong cõi người ta
    <<<<<<< HEAD
    chữ sinh chữ mệnh khéo là ghét nhau
    =======
    chữ tài chữ mệnh khéo là thích nhau
    >>>>>>> a

Có thể thấy 7 dấu bằng phân cách 2 phiên bản khác nhau. `HEAD` là phiên bản ở nhánh
hiện tại (nhánh b) còn `a` là phiên bản ở nhánh `a`. Để resolve chúng ta chọn
một phương án phù hợp nhất từ 2 phương án. Rồi xóa những ký hiệu do git để lại
trong file (ở đây chúng ta chọn phương án sử dụng cả 2 branch):

    Trăm năm trong cõi người ta
    Chữ sinh chữ mệnh khéo là thích nhau

Sau đó commit file này (vì lệnh merge không thành công tạo tình huống dở chừng
trong repo):

    git add kieu
    git commit

Git sẽ hiện ra giao diện commit với một commit message được tạo sẵn kiểu ntn:

    Merge branch 'a' into b

    Conflicts:
            kieu

Giữ nguyên hoặc thêm gì nếu muốn và tiếp tục commit (nhấn Escape, sau đó gõ :wq
oy Enter).

<h2 id="jekyll">Jekyll</h2>
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

Đây là một ví dụ thực tế hơn:

    default.html:

    <!DOCTYPE html>
    <html>
      <head>
        <title>{{ page.title }}</title>
        <meta name="description" content="{{ page.description }}"/>
        <!-- Bootstrap -->
        <link href="css/bootstrap.min.css" rel="stylesheet" media="screen">
      </head>
      <body>
          <header>
            Header
          </header>
          
          <article>
            {{ content }}
          </article>
          
          <footer>
            Footer
          </footer>

        
        <!-- Scripts -->
        <script src="http://code.jquery.com/jquery-latest.js"></script>
        <script src="js/bootstrap.min.js"></script>
      </body>
    </html>


    index.html:
        
    ---
    layout: default
    title: "iPhone 6"
    description: "iPhone 6 is the lastest iteration in our world-renowned iPhone
    product lines."
    ---

    <h1>Hello, world!</h1>

sẽ tạo ra kết quả như thế này:


    <!DOCTYPE html>
    <html>
      <head>
        <title>iPhone 6</title>
        <meta name="description" content="iPhone 6 is the lastest iteration in our world-renowned iPhone product lines."/>
        <!-- Bootstrap -->
        <link href="css/bootstrap.min.css" rel="stylesheet" media="screen">
      </head>
      <body>
          <header>
            Header
          </header>
          
          <article>
            <h1>Hello, world!</h1>

          </article>
          
          <footer>
            Footer
          </footer>

        
        <!-- Scripts -->
        <script src="http://code.jquery.com/jquery-latest.js"></script>
        <script src="js/bootstrap.min.js"></script>
      </body>
    </html>


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

<h2 id="bootstrap">Bootstrap</h2>

[Bootstrap](http://twitter.github.com/bootstrap/) là một tập hợp các file css, js
và hình ảnh được thiết kế sẵn để giúp tăng tốc quá trình build giao diện cho một
website. Nhiều vấn đề khó như tạo layout bằng grid, animation, widget, responsive
design đã được Bootstrap thiết kế trước nên giảm bớt gánh nặng cho lập trình viên
một cách đáng kể.

Hướng dẫn sử dụng Bootstrap có thể tìm hiểu tại [đây](http://twitter.github.com/bootstrap/getting-started.html)
