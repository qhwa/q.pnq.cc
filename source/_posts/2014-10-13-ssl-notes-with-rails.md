上周我给[小兔盒](https://xiaotuhe.com)加上了https，比想象中容易许多。记录一下

### 免费的CA: 
之前一直以为 CA 是需要每年付一笔不菲的费用的，但其实也有免费的，例如：
https://www.startssl.com/

按照网站指示，可以获得由其颁发的证书 有两个文件(certification & key) 是后面工作的基础。

### 在开发环境中使用 https (无需nginx)

{% codeblock lang:sh %}
thin start --ssl --ssl-key-file YOUR_SSL_KEY_FILE --ssl-cert-file YOUR_CERT_FILE
{% endcodeblock %}

### 一些 tips

#### url helpers

不管当前 request 是 https 还是 http，rails 的 url_helper 都使用 http

{% codeblock lang:ruby %}
# file: config/routes:
root to: 'home#index'

# in views or helpers:
root_url                    #=> http://YOUR_SITE/
root_url protocol: 'https'  #=> https://YOUR_SITE/
{% endcodeblock %}

#### 使用 protocol 无关的 assets 地址

{% codeblock lang:ruby %}
# file: config/environments/production.rb
Rails.application.configure do
  ...
  config.action_controller.asset_host = '//YOUR-CDN.com'
  ...
end
{% endcodeblock %}

