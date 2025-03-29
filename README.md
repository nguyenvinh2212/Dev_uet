# Dev_uet
1. Giới thiệu
Dự án game này được xây dựng bằng ngôn ngữ C++ sử dụng thư viện SDL2, với mục tiêu tạo ra một trò chơi hành động kết hợp các yếu tố như:

Điều khiển nhân vật (Player) với hiệu ứng animation cho động cơ và hiệu ứng bảo vệ (shield).

Quản lý các đối tượng kẻ thù (Enemy) với nhiều hành vi di chuyển khác nhau (di chuyển zig-zag, lượn sóng, di chuyển chéo, boss, ...).

Tích hợp hệ thống menu với các tùy chọn như Start, Options, Controls, High Score và Exit.

Hỗ trợ âm thanh và hiệu ứng đồ họa.

2. Mô tả kiến trúc và cấu trúc dự án
2.1. Các thành phần chính
Main Loop và Input Handling:

Hàm main() là điểm khởi đầu của chương trình, xử lý vòng lặp game, cập nhật logic, vẽ đồ họa và giới hạn FPS.

Hàm doInput() xử lý các sự kiện từ bàn phím (SDL_QUIT, SDL_KEYDOWN, SDL_KEYUP, SDL_TEXTINPUT) và cập nhật trạng thái điều khiển.

Quản lý Game State và Menu:

Biến toàn cục gameState xác định game đang ở trạng thái chơi hay hiển thị menu chính.

Các đối tượng như Menu menu, Stage stage quản lý giao diện và logic chuyển đổi giữa các menu (Main, Options, Controls, High Score).

Menu được xây dựng với các item có ảnh hưởng đến hành động như Start, Options, Back… và thay đổi bằng phím UP/DOWN, ENTER.

Xử lý đối tượng trong game:

Player:

Quản lý nhân vật chính với các thuộc tính như vị trí, tốc độ, sức khỏe và trạng thái shield.

Sử dụng lớp Animation để tạo hiệu ứng cho động cơ (tail) và hành tinh (plannet) bên cạnh hiệu ứng shield.

Hàm clip() giới hạn vị trí nhân vật không vượt quá biên màn hình.

Enemy:

Đối tượng kẻ thù có nhiều loại hành vi khác nhau được phân theo biến wave và giá trị wave % 7.

Mỗi loại Enemy có các chuyển động độc đáo (zig-zag, lượn sóng, di chuyển chéo, boss, …) và được gán texture riêng.

Hàm update() xử lý logic di chuyển và phản hồi khi va chạm biên màn hình.

Hệ thống Animation:

Lớp Animation chịu trách nhiệm xử lý các khung hình (frame) của đối tượng động.

Hàm update() cập nhật frame dựa trên thời gian trôi qua và có tùy chọn lặp lại (repeat) hay không.

Hàm render() thực hiện việc vẽ animation lên renderer.

Quản lý HighScore:

Lớp HighScoreManager dùng để lưu trữ và xử lý bảng điểm cao, đọc ghi file "Highscore.txt".

Phương thức addScore() thêm điểm mới và duy trì bảng điểm cao gồm 5 mốc cao nhất.

3. Lối chơi và logic game
Gameplay:

Người chơi điều khiển nhân vật bằng bàn phím, tránh va chạm với kẻ thù và có thể kích hoạt shield bảo vệ tạm thời.

Kẻ thù xuất hiện theo các dạng hành vi khác nhau, làm tăng độ khó của trò chơi khi game tiến triển.

Khi tạm dừng game (bằng phím ESC), menu pause xuất hiện với lựa chọn “Continue” và “Back to Menu”.

Hiệu ứng âm thanh – đồ họa:

Âm lượng của game và nhạc được điều chỉnh thông qua menu Options bằng các phím trái/phải.

Hiệu ứng animation cho nhân vật và kẻ thù được cập nhật liên tục theo deltaTime, giúp chuyển động mượt mà.

Background và các texture được load từ các file hình ảnh như "Image/enemy1.png", "Image/menu/start.png", "Image/Title.png",…

4. Cấu trúc project
Các file chính:

main.cpp: Chứa vòng lặp chính, xử lý input và logic game.

Game_object.h/cpp: Định nghĩa các lớp đối tượng game như Player và Enemy.

Animation.h/cpp: Xử lý các hiệu ứng animation.

Menu.h/cpp: Xây dựng hệ thống menu (Main, Options, Controls, HighScore).

HighScore.h/cpp: Quản lý bảng điểm cao.

Common.h/cpp: Các hàm hỗ trợ như loadTexture, xử lý va chạm, và tính toán vector.

Quản lý tài nguyên:

Các hình ảnh (texture) và âm thanh được lưu trong các thư mục riêng (Image, animation, font).

File "Highscore.txt" dùng để lưu trữ dữ liệu điểm cao.

5. Các chức năng đã cài đặt
Điều khiển nhân vật và hiệu ứng:

Di chuyển nhân vật, giới hạn vị trí trong màn hình.

Hiệu ứng động cơ (tail) và bảo vệ (shield) được xử lý qua lớp Animation.

Đa dạng đối tượng kẻ thù:

Các loại Enemy với hành vi di chuyển đa dạng (zig-zag, lượn sóng, di chuyển chéo, boss).

Cập nhật trạng thái và logic di chuyển riêng biệt cho từng loại.

Hệ thống menu và điều khiển:

Menu chính với các lựa chọn: Start, Options, Controls, High Score, Exit.

Menu Options cho phép điều chỉnh âm lượng của game và nhạc.

Menu điều khiển (Controls) cung cấp hướng dẫn về cách chơi.

Menu HighScore hiển thị bảng điểm cao được lưu trong file.

Xử lý âm thanh và FPS:

Điều chỉnh âm lượng dựa trên giá trị soundVolume và musicVolume.

Giới hạn FPS đảm bảo game chạy mượt mà.

Các hàm hỗ trợ:

Hàm collision() kiểm tra va chạm giữa các đối tượng.

Hàm calcSlope() tính toán vector chuyển động giữa 2 điểm.

6. Kết luận và hướng phát triển
6.1. Đánh giá dự án:
Ưu điểm:

Cấu trúc dự án rõ ràng, phân chia module hợp lý (menu, game object, animation, highscore).

Xử lý hiệu ứng animation mượt mà, hỗ trợ nhiều loại đối tượng với logic di chuyển độc đáo.

Hệ thống menu đa dạng, tích hợp điều chỉnh âm lượng và hiển thị bảng điểm cao.

Hạn chế:

Một số đoạn code lặp lại (ví dụ: phần khởi tạo của Player và Enemy) có thể tối ưu lại bằng cách tái cấu trúc.

Cần kiểm tra và xử lý các trường hợp ngoại lệ (ví dụ: lỗi load texture, quản lý bộ nhớ) kỹ hơn.

Phần xử lý input và update menu có thể bổ sung thêm các hiệu ứng chuyển động hoặc âm thanh phản hồi.

6.2. Hướng phát triển tương lai:
Tối ưu hóa mã nguồn, giảm thiểu việc lặp lại code qua việc sử dụng các hàm chung.

Mở rộng tính năng game: thêm cấp độ, boss mới, hoặc chế độ chơi đa người.

Nâng cao hiệu ứng đồ họa, tích hợp hiệu ứng ánh sáng và bóng tối.

Cải thiện giao diện người dùng cho các menu, tăng tính tương tác.


    
