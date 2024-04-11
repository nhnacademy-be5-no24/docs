## WYSIWYG Editor 적용 및 사용방법

1. API KEY 발급
- https://www.tiny.cloud/my-account/integrate/#html
- 위 사이트에 접속 / 로그인 후, API KEY를 발급 받는다.

2. thymeleaf head에 아래의 코드를 넣는다.
```javascript

<head>
...
<script src="https://cdn.tiny.cloud/1/{발급받은 API_KEY}/tinymce/7/tinymce.min.js" referrerpolicy="origin"></script>
<script>
    tinymce.init({
        selector: '#bookDescription',  <!-- querySelector처럼 활용하여, textarea의 id를 가져온다. -->
        height: 300,
        <!-- 플러그인 내용, 툴바 내용 Customizing -->
        plugins: [
            'advlist autolink lists link image charmap print preview anchor',
            'searchreplace visualblocks code fullscreen',
            'insertdatetime media table paste code help wordcount'
        ],
        toolbar: 'undo redo | formatselect | ' +
            'bold italic backcolor | alignleft aligncenter ' +
            'alignright alignjustify | bullist numlist outdent indent | ' +
            'removeformat | help',
        content_style: 'body { font-family: Arial, Helvetica, sans-serif; font-size: 14px }'
    });
</script>
</head>
<body>
    <!-- thymeleaf에 WYSIWYG 적용하고 싶다면, 아래와 같이 코드 작성 -->
    <div class="form-group">
        <label for="bookDescription">설명</label>
        <textarea name="bookDescription" id="bookDescription" placeholder="책 설명 입력"></textarea>
    </div>

    <!-- 태그와 함께 불러오고 싶다면, th:utext를 활용한다. -->
    <div th:utext="${bookDescription}"></div>
</body>
```

3. 결과
   <img width="996" alt="image" src="https://github.com/nhnacademy-be5-no24/docs/assets/43560497/f991b03a-db62-4d74-9dc6-0f5bbb222c23">
   <img width="1002" alt="image" src="https://github.com/nhnacademy-be5-no24/docs/assets/43560497/73f3171f-812e-4a99-8f35-bdc6b17308b9">

