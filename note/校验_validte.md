Validate

    作用是：当用户提交的信息格式错误时：会按照你在validate
    面设置好的信息提醒用户格式的错误。
    
一般Validate文件会放在controller文件夹里面
    
    在validate文件夹的php文件中一般都会默认先执行
    protected $rule = [
            'name' => 'require|max:25',
            'email' => 'email',
            'logo' => 'require',
            'city_id' => 'require',
            'bank_info' => 'require',
            'bank_name' => 'require',
            'bank_user' => 'require',
            'faren' => 'require',
            'faren_tel' => 'require',
        ];
    
    
    在场景设置中，你可以对上面$rule设置的属性，进行筛选行的进行校验
    /**场景设置**/
    protected  $scene = [
            'add' => ['name', 'email', 'logo', 'city_id', 'bank_info', 'bank_name', 'bank_user', 'faren', 'faren_tel'],
        ];
    
在controller控制台调用时：

    $data = input('post.')//接收前端穿过来的信息
    $validate = validate('Category(在validate中的php文件名)')；
    //默认调用$rule
    $validate->check($data)
    //不想对rule里面的所有属性进行校验时，可以调用scene里面自己设置好的属性
    $validate->scene('add')->check($data) 
        
    