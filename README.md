## hexo s
	启动服务
## hexo g
	生成静态文件，每次需要更新博客之前都需要执行生成public静态文件
## hexo clean
	删除缓存，即删除public文件
## hexo d
	部署本地数据到远程服务

### banner
	1. 首页banner每天一张，各gif与jpg各有7张，可以随时切换，文件地址在\themes\matery\source\medias，生成文件在themes/layout/_partial/bg-cover-content.ejs
	2. banner图最好不要有radios，因为banner有默认颜色，有radios的话，默认背景颜色会显示出来不好看

### 相册
	1. 相册生成文件在\themes\matery\layout\gallery.ejs，
	2. 配置文件在\source\_data\galleries.json，配置文件里面图片路径放的是带域名的全部链接，这样就不需要在gallery.ejs里面做不同相册的判断，直接使用路径就行
	3. 相册的展示样式与\source\_data\galleries.json文件中的water-fall这个类旁边的那个id的类encrypt-blog有关，加上与去掉两种类型，不加的话是类似于瀑布流的（实际不是），非等高，加上就是等高的样式https://github.com/Luoyangz/Luoyangz.github.io.git