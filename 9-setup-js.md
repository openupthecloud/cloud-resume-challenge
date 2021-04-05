## Progress

1.  ✅ Certification
2.  ✅ HTML
3.  ✅ CSS
4.  ✅ Static S3 Website
5.  ✅ HTTPS
6.  ✅ DNS
7.  ✅ Javascript
8.  ❌ Database
9.  ✅ API
10. ❌ Python
11. ❌ Tests
12. ✅ Infrastructure as Code
13. ✅ Source Control
14. ❌ CI/CD (Back end)
15. ❌ CI/CD (Front end)
16. ❌ Blog post

## Setup JS

```javascript
<script>
    fetch('https://92pa1yuyzc.execute-api.us-east-1.amazonaws.com/Prod/hello')
        .then(response => response.json())
        .then((data) => {
            document.getElementById('replaceme').innerText = data.count
        })
</script>
```
