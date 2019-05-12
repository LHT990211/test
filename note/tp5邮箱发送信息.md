tp5邮箱发送信息
        
   phpmailer 安装或者下载方式:
  
   1、从 github 上下载: https://github.com/PHPMailer/PHPMailer/
    放在tp5/extend里面
      
      控制器代码：  
        <?php
        
        namespace app\admin\controller;
        
        use think\Controller;
        use PHPMailer\PHPMailer\PHPMailer;
        use PHPMailer\PHPMailer\Exception;
        
        class Email extends Controller
        {
            /**
             * 显示资源列表
             *
             * @return \think\Response
             */
            public function index($eamil,$title,$content)
            {
                import('phpmailer.src.Exception', EXTEND_PATH);
                import('phpmailer.src.PHPMailer', EXTEND_PATH);
                import('phpmailer.src.SMTP', EXTEND_PATH);
        
                $mail = new PHPMailer();
        //        exit();
                try {
                    //服务器配置
                    $mail->CharSet ="UTF-8";                     //设定邮件编码
                    $mail->SMTPDebug = 0;                        // 调试模式输出
                    $mail->isSMTP();                             // 使用SMTP
                    $mail->Host = 'smtp.163.com';                // SMTP服务器
                    $mail->SMTPAuth = true;                      // 允许 SMTP 认证
                    $mail->Username = '15876766724@163.com';                // SMTP 用户名  即邮箱的用户名
                    $mail->Password = 'lht990211';             // SMTP 密码  部分邮箱是授权码(例如163邮箱)
                    $mail->SMTPSecure = 'ssl';                    // 允许 TLS 或者ssl协议
                    $mail->Port = 465;                            // 服务器端口 25 或者465 具体要看邮箱服务器支持
        
                    $mail->setFrom('15876766724@163.com', 'Mailer');  //发件人
                    $mail->addAddress($eamil, 'Joe');  // 收件人
                    //$mail->addAddress('ellen@example.com');  // 可添加多个收件人
                    $mail->addReplyTo('15876766724@163.com', 'info'); //回复的时候回复给哪个邮箱 建议和发件人一致
                    //$mail->addCC('cc@example.com');                    //抄送
                    //$mail->addBCC('bcc@example.com');                    //密送
        
                    //发送附件
                    // $mail->addAttachment('../xy.zip');         // 添加附件
                    // $mail->addAttachment('../thumb-1.jpg', 'new.jpg');    // 发送附件并且重命名
        
                    //Content
                    $mail->isHTML(true);                                  // 是否以HTML文档格式发送  发送后客户端可直接显示对应HTML内容
                    $mail->Subject = $title;
                    $mail->Body    = '<h1>.$content.</h1>' . date('Y-m-d H:i:s');
                    $mail->AltBody = '如果邮件客户端不支持HTML则显示此内容';
        
                    $mail->send($eamil,$title,$content);
                    echo '邮件发送成功';
                } catch (Exception $e) {
                    echo '邮件发送失败: ', $mail->ErrorInfo;
                }
        
            }
        
        
        
        
        }