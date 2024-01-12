```
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>Laravel</title>

    // اینو بالای اون جایی که میخوای dropzone داشته باشی اضافه کن 
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/dropzone/5.9.3/min/dropzone.min.css"
        integrity="sha512-WvVX1YO12zmsvTpUQV8s7ZU98DnkaAokcciMZJfnNWyNzm7//QRV61t4aEr0WdIa4pe854QHLTV302vH92FSMw=="
        crossorigin="anonymous" referrerpolicy="no-referrer" />
</head>
<body class="antialiased">
    <h1>welcome page</h1>
    <form method="post" action="{{ route('upload') }}" enctype="multipart/form-data" class="dropzone" id="dropzone">
        @csrf
        <div class="dz-message">
            <div class="col-xs-8">
                <div class="message">
                    <p>Drop files here or Click to Upload</p>
                </div>
            </div>
        </div>
        <div class="fallback">
            <input name="file" type="files" multiple accept="image/jpeg, image/png, image/jpg" />
        </div>
    </form>
    // اینو پایین اون جایی که میخوای dropzone داشته باشی اضافه کن
    <script src="https://cdnjs.cloudflare.com/ajax/libs/dropzone/5.9.3/min/dropzone.min.js"
        integrity="sha512-oQq8uth41D+gIH/NJvSJvVB85MFk1eWpMK6glnkg6I7EdMqC1XVkW7RxLheXwmFdG03qScCM7gKS/Cx3FYt7Tg=="
        crossorigin="anonymous" referrerpolicy="no-referrer"></script>
    // این کد میاد اون فایل یا فایلهای انتتخاب شده رو میفرسته سمت بک اند برای ذخیره سازی
    <script charset="utf-8">
        Dropzone.options.dropzone = {
            maxFilesize: 12,
            //maxFiles: 1,
            renameFile: function(file) {
                return file.name;
            },
            acceptedFiles: ".jpeg,.jpg,.png",
            addRemoveLinks: false,
            timeout: 5000,
            success: function(file, response) {
                return console.log(response);
            },
            error: function(file, response) {
                return console.log(response);
            }
        };
    </script>
</body>
</html>
```


#### این متد میاد و اون فایل رو برات توی جدول ذخیره میکنه و تمام

```
public function upload(Request $request)
{
    $file = $request->file('file');

    $address = $file->store('image');

    DB::table('images')->insert([
        'user_id' => 1,
        'image' => $address,
    ]);

    return response(true, 200);
}
```
