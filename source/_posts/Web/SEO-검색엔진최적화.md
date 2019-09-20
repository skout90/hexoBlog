---
title: 검색 엔진 최적화 SEO
date: 2017-08-15 19:28:10
categories:
    - Web
---

## 검색 엔진 최적화 SEO

SEO(Search Engine Optimize) : 검색 엔진 최적화, 구글 엔진이 크롤링 보다 잘 하기 위해서 최적화가 필요.

- 명확하고 동창적 title 태그 사용.
- description 메타태그 활용하기
- URL 구조 개선
- ..

### canonical

````html
<head>
	<link rel="canonical" href="http://www.seo-korea.com" />
</head>
````

표준 URL을 설정함으로써, 검색엔진이 URL을 쉽게 최적화하여, PageRank 상승에 기여하고, 중복된 컨텐츠를 쉽게 없엘 수 있음.

### sitemap.xml

루트에 sitemap.xml 파일 만들어 놓기 `abc.com/sitemap.xml`

- sitemap.xml

````xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="sitemap.xsl"?>
<sitemapindex xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    <sitemap>
        <loc>https://skout90.github.io/post-sitemap.xml</loc>
        <lastmod>2017-07-11T07:52:30.093Z</lastmod>
    </sitemap>
    <sitemap>
        <loc>https://skout90.github.io/page-sitemap.xml</loc>
        <lastmod>2017-07-11T07:52:32.290Z</lastmod>
    </sitemap>
    <sitemap>
        <loc>https://skout90.github.io/category-sitemap.xml</loc>
        <lastmod>2017-07-11T07:52:07.793Z</lastmod>
    </sitemap>
</sitemapindex>
````

- page-sitemap.xml

````xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="sitemap.xsl"?>
<urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:image="http://www.google.com/schemas/sitemap-image/1.1" xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd" xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    <url>
        <loc>https://skout90.github.io</loc>
        <changefreq>daily</changefreq>
        <priority>1</priority>
    </url>
    <url>
        <loc>https://skout90.github.io/all-categories/</loc>
        <lastmod>2017-07-11T07:52:32.290Z</lastmod>
        <changefreq>weekly</changefreq>
        <priority>0.8</priority>
    </url>
</urlset>
````

### 구글 Search Console 등록

https://www.google.com/webmasters/tools/home

내 URL을 등록하고, 위의 sitemap.xml도 함께 등록해주자.



## Reference

http://www.aun-korea.com/%EB%A7%88%EC%BC%80%ED%84%B0%EC%83%81%EC%8B%9D-%EB%84%A4%EC%9D%B4%EB%B2%84-%EA%B5%AC%EA%B8%80%EC%97%90-%EA%B2%80%EC%83%89%EB%85%B8%EC%B6%9C%EC%9D%B4-%EC%9E%98%EB%90%98%EA%B2%8C-%ED%95%98%EB%8A%94/

[http://tobeonline.tistory.com/entry/구글이-제시하는-검색엔진-최적화SEO-방법]()

http://www.seo-korea.com/%ED%91%9C%EC%A4%80-%ED%8E%98%EC%9D%B4%EC%A7%80-%EC%84%A4%EC%A0%95-link-rel-canonical/

http://futurecreator.github.io/2016/06/15/hexo-google-site-search-console-analytics/