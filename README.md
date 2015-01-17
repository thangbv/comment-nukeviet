# comment-nukeviet
Module comment for NukeViet 4.0
- Thêm cột url_comment phục vụ việc xem bài viết hoặc url được comment tương tự facebook
- Loại bỏ Iframe của module hiện tại
- Thay đổi kiểu từ tinyint sang int của cột area

--Hướng dẫn chỉnh sửa
- Loại bỏ heesrt các phần comment hiện tại đang dùng của NukeViet 
Tại khu vực muốn comment thêm đoạn sau
```
// comment
	define( 'NV_COMM_ID', $id_content );//ID bài viết hoặc 
	define( 'NV_COMM_AREA', $module_info['funcs'][$op]['func_id'] );//để đáp ứng comment ở bất cứ đâu không cứ là bài viết
	//check allow comemnt
	$allowed = $module_config[$module_name]['allowed_comm'];//tuy vào module để lấy cấu hình. Nếu là module news thì có cấu hình theo bài viết
	if( $allowed == '-1' )
	{
		$allowed = ( defined( 'NV_COMM_ALLOWED' ) ) ? NV_COMM_ALLOWED : $module_config[$module_name]['setcomm'];
	}
	define( 'NV_PER_PAGE_COMMENT', 5 ); //Số bản ghi hiển thị bình luận
	require_once NV_ROOTDIR . '/modules/comment/comment.php';
	$area = ( defined( 'NV_COMM_AREA' ) ) ? NV_COMM_AREA : 0;
	$checkss = md5( $module_name . '-' . $area . '-' . NV_COMM_ID . '-' . $allowed . '-' . NV_CACHE_PREFIX );

	//get url comment
	$url_info = parse_url( $client_info['selfurl'] );
	$url_comment = $url_info['path'];
	
	$content_comment = nv_comment_module( $module_name, $url_comment, $checkss, $area, NV_COMM_ID, $allowed, 1 );// hàm này trả về nội dung html vậy nên chỉ cần truyền 1 biến vào function của theme và gán Assign tempalte là được
```
