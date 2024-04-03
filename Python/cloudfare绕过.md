1. 使用cloudscraper
```python
import cloudscraper
scraper = cloudscraper.create_scraper(browser={'browser': 'chrome', 'platform': 'windows', 'mobile': False})
# 在此之后用法与requests大致无异
```
2. 使用undetected_chromedriver来使其绕过？（雾）不太会用
3. cfscrape好像也能用