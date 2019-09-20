---
title: 파일 업로드를 위한 blob 객체 컨트롤
date: 2018-08-24 19:28:10
categories:
    - Node.js
---

- front
````javascript
    //blob 객체가 존재한다고 가정
	const formData = new FormData()

    formData.append('file', blob, 'filename.jpg')
    formData.append('subPath', 'shop')

    const res = await axios.post(`/file`, formData)
````



- backend

connect-multiparty 라는 npm을 사용하면, multipart로 전송된 파일을 /tmp/blabla.확장자  경로에 저장해준다.

그 후, 임시 저장된 경로를 file object에 넣어서 return 해주는 백엔드 코드.

````javascript
const router = require('express').Router()
const multipart = require('connect-multiparty')
const multipartMiddleware = multipart()

router.post('/', multipartMiddleware, errorHandler(async (req, res, next) => {
  res.json({
    file: _.extend(req.files.file, {subPath: req.body.subPath})
  })
}))

module.exports = router
````

