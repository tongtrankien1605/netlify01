## tiktok-clone-v3 by Tống Trần Kiên

</br>

## 🏆 Đây là code base, có thể sử dụng để xây dựng phát triển thêm các chương trình lớn hơn

    - Mỗi lần truy cập sẽ tải dữ liệu video từ ( server lưu trữ video CDN jsDelivr ) để xem, không cache video vào Service
    Worker vì đã sử dụng CDN (  Content Delivery Network )

    - Service Worker chỉ cache các dữ liệu tĩnh ( html, css,... ) và không cache dữ liệu động ( video,... ) -> Nhiều video
    cũng không gây tốn cache vì chỉ cache dữ liệu tĩnh có dung lượng nhỏ

    - Note 1: Khi lưu trữ video bằng CDN thì không tính băng thông cho Github Page. Do đó, sau khi thoát ra, và khi truy cập
    lại sẽ lại tải từ server để xem theo trình tự như vậy

    - Note 2: Tuy nhiên CDN jsDelivr có cơ chế cache HTTP 7 ngày, Nên do đó có thể tận dụng và xem lại video từ cache HTTP mà
    không cần tải lại từ server CDN cho đến khi cache hết hạn

    - Note 3: Trong videos.json có thể dùng 3 dạng link gồm ( link CDN jsDelivr, link base github chứa /blob , link raw github ).
    Có logic xử lý để tự động chuyển đổi ánh xạ link base & link raw sang link CDN để tải dữ liệu băng thông không giới hạn

    - Note 4: Khi đã upload video lên github, muốn thay đổi video mới. THÌ Xóa video cũ + Add video mới ( phải trùng tên ) + Commit
    -> tiếp tục Purge Cache tại (  https://www.jsdelivr.com/tools/purge  ) -> Update version -> Chờ khoảng 5 - 10p -> Done

    - Note 5: Sử dụng ( baseConfig & hostname ) để cấu hình các BASE_URL dùng cho github page và cả các host khác như netlify,...

    - Note 6: Sử dụng window.location.pathname ( html ) & self.registration.scope ( service worker ) để lấy pathname dùng cho
    basepath cho REPOSITORY_ROOT đối với Github Pages và Gitlab Pages

    - Note 7: Cấu hình sẵn baseConfig để ánh xạ lấy basepath đối với các dịch vụ: Netlify ( netlify.app ), Vercel ( vercel.app ),
    Cloudflare ( pages.dev ), Firebase Hosting ( web.app ), Surge ( surge.sh ), Neocities ( neocities.org ), Render ( onrender.com ).
    Bên cạnh đó 2 dịch vụ Github Pages ( github.io ) & Gitlab Page ( gitlab.io ) được cấu hình sẵn base path tự động qua URL

</br>

## 🫣 Các giới hạn được thu thập được trong quá trình tester

    - Giới hạn up file trực tiếp ở web của github là 25 MB ( Yowza, that’s a big file. Try again with a file smaller than 25MB )

    - Github gửi cảnh báo khi up file vượt 50 MB ( This is larger than GitHub's recommended maximum file size of 50.00 MB )

    - Giới hạn up push file qua vscode của github là 100 MB ( This exceeds GitHub's file size limit of 100.00 MB )

    - Giới hạn file của CDN jsDelivr hỗ trợ tối đa là 20MB ( File size exceeded the configured limit of 20 MB )

</br>

## 💻 Giải thích các BASE_URL:

    const REPOSITORY_ROOT: Đường dẫn gốc của dự án, dùng để đăng ký Service Worker.
    ( ví dụ xây dựng trên github có repository là tiktok-clone-v3 => thì REPOSITORY_ROOT = "/tiktok-clone-v3/" )

    const VIDEOS_JSON_URL: Đường dẫn đến file JSON chứa thông tin video như Title, URL, Desription, dayCreate
    ( ví dụ xây dựng trên github có repository là tiktok-clone-v3 => thì const VIDEOS_JSON_URL = `${REPOSITORY_ROOT}videos.json`; )

    const CACHE_NAME: Tên của Worker Service, lưu ý cần cập nhật ở cả file html & script. ( const CACHE_NAME = "service-worker-v1" )

</br>

## ❌ Cách xóa Local Storage, Cache Service Worker, Cache HTTP:

    Settings -> Privacy and security -> Delete browsing data -> Cached images and files : Xóa Cache HTTP
    ( Cài đặt -> Quyền riêng tư và bảo mật -> Xóa dữ liệu duyệt web -> Tệp và hình ảnh được lưu trong bộ nhớ đệm )

    F12 -> Application -> Local storage : xóa Local Storage

    F12 -> Application -> Cache storage : xóa Cache Service Worker

</br>
