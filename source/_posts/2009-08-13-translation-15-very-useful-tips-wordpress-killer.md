--- 
categories: 
  - "about blog"
  - WordPress
comments: true
layout: post
published: true
status: publish
tags: 
  - blog
  - hack
  - WordPress
title: 翻译：15个非常有用的杀手级WordPress技巧
type: post
---
原文作者：www.wpbeginner.com
原文链接：<a href="http://www.wpbeginner.com/wp-tutorials/15-killer-hacks-for-wordpress-that-are-extremely-useful/" target="_blank">15 Killer Hacks for WordPress that Are Extremely Useful</a>
<span class="alert_font">友情提示：请想尝试以下技巧的朋友在复制相关代码的时候注意单引号的全角半角问题，本人在应用过程中曾遇到过类似问题。</span>
WordPress的社区正在迅速扩张，我们每天都在推出新的技巧。在本文中，我们将与你们分享一些杀手级的，用户最想要的，以及非常有用的WordPress技巧。您可以使用这些技巧来释放WordPress，这个我们都深深喜爱的博客软件的更多力量。我们将尝试解释每个技巧是如何起作用的。
<span class="inner_title">1、从日志的标题链接到外部链接</span>
通常有这样的情况，Blogger希望可以链接到一个外部链接，因为他/她认为那是有益于读者的。主要的问题是，必须发布一个新日志，以便告诉读者去到其他网站。我们将告诉您如何利用此自定义字段技巧，从日志的标题链接到一个外部链接。
<!--more-->
第一件事你需要做的就是，打开您的主题文件所在文件夹中的functions.php这个文件。然后粘贴以下代码：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

现在，您需要打开您的index.php ，找到下面的代码或类似的东西：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

更改为：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

您做好了这些后，将这两个文件上传到您的主机上覆盖原文件。
现在，当您在管理后台撰写文章时，向下滚动到自定义字段。找到名称：url1，title_url ，或url_title，添加外部链接，增加您想要的简短说明，然后发布。
不要害怕，这个功能并没有去除您正常的日志的链接，它所做的只是增加一个额外的查询，检查自定义字段的外部链接。如果外部链接不存在，它就会链接到正常的日志页面。
还有一个插件可以达到同样的功能，插件名：<a href="http://txfx.net/code/WordPress/page-links-to/" target="_blank">Page Links To</a>。
<span class="inner_title">2、更改评论里默认的Gravatar</span>

<a href="http://www.hopes4.me/images/uploads/2009/08/goodbye.gif"><img style="display: block; float: none; margin-left: auto; margin-right: auto; border: 0px;" title="Good Bye Mystery Man" src="http://www.hopes4.me/images/uploads/2009/08/goodbye_thumb.gif" border="0" alt="Good Bye Mystery Man" width="484" height="84"></a>
默认的mystery man实在是困扰着大多数用户。另外如果有更多的机会可以修改化您的博客，那么为什么不这样做呢。更改默认的gravatar可以让您的博客更有个性。通过下面的代码片段，您就可以更改默认的gravatar 。
首先您需要打开您的主题文件所在文件夹中的functions.php这个文件。如果没有您可以创建一个，然后插入以下代码：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

在代码中，图片从主题文件夹中提取出来，这是所谓的gravataricon.gif，显然您将会把它改为您的图片名称。如果选择了WPBeginner ，这是名称所代表的avatar将会显示在您的管理面板的选项区域。
<a href="http://www.hopes4.me/images/uploads/2009/08/gravatarsettings.gif"><img style="display: block; float: none; margin-left: auto; margin-right: auto; border: 0px;" title="Gravatar Settings" src="http://www.hopes4.me/images/uploads/2009/08/gravatarsettings_thumb.gif" border="0" alt="Gravatar Settings" width="484" height="296"></a>
回到您的管理面板，点击设置 >讨论，然后修改图标，这样您就会有一个带有您的标志的个性化的评论区。
<span class="inner_title">3、显示个性化的Retweet按钮</span>
<a href="http://www.hopes4.me/images/uploads/2009/08/retweet.gif"><img style="display: block; float: none; margin-left: auto; margin-right: auto; border: 0px;" title="Add a Retweet button in WordPress" src="http://www.hopes4.me/images/uploads/2009/08/retweet_thumb.gif" border="0" alt="Add a Retweet button in WordPress" width="484" height="154"></a>
Twitter获得如此多的曝光，作为一个Blogger您应该已经用它来发挥您的优势了。Twitter有着其他宣传方式所没有的力量，因为它是口耳相传的广告。为了方便您的读者，您可以做的一个突出的Retweet按钮，这样他们就可以一键retweet您的文章了。不仅如此，您还应该用适当的方式，来跟踪Retweets。这就是tweetmeme这个插件的用处所在。
本指南中我们将创建一个按钮，其链接的文本格式如下：
RT @您的网站名 日志标题 – 链接
将下面的代码添加到您的主题文件所在文件夹中的single.php内
大按钮：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

简洁的按钮：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

记得把tweetmeme_source改成您自己的Twitter帐户名称，这样你不仅会促进您的帐户获得更多的追随者，同是您的日志也将得到促进。
<span class="inner_title">4、随机显示您blog的标题图片</span>
<a href="http://www.hopes4.me/images/uploads/2009/08/randomheaderimages.gif"><img style="display: block; float: none; margin-left: auto; margin-right: auto; border: 0px;" title="Random Header Images" src="http://www.hopes4.me/images/uploads/2009/08/randomheaderimages_thumb.gif" border="0" alt="Random Header Images" width="484" height="111"></a>
大多数博客的设计让人感觉沉闷，是因为它们有一个巨大的标题图片，而且它还是静态的。本教程可以使您的标题图像动态展示，因为它在用户每次访问时轮流显示标题图片。你可以选择尽可能多的想随机轮换的图片，它将给您的博客带来生趣。
首先，您必须按下面的格式为您的图像命名：

<ul>
<li>headerimage_1.gif</li>
	<li>headerimage_2.gif</li>
	<li>headerimage_3.gif</li>
</ul>必须用下划线来分隔图片的名称，您可以将headerimage更改为himage或任何您喜欢的其他文字。
完成上述工作后，您需要将下面的代码粘贴到您的header.php中您想要的图片显示的位置或其他任何文件。


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

如果您决定要放上多于3张的图片，请修改数字3。这个代码并不是排他性的，只针对WordPress，它适用于任何PHP平台。
<span class="inner_title">5、控制日志出现在RSS上的时间</span>
<a href="http://www.hopes4.me/images/uploads/2009/08/rsstimecontrol.gif"><img style="display: block; float: none; margin-left: auto; margin-right: auto; border: 0px;" title="Control When Your Posts are Available Via RSS" src="http://www.hopes4.me/images/uploads/2009/08/rsstimecontrol_thumb.gif" border="0" alt="Control When Your Posts are Available Via RSS" width="484" height="154"></a>
有些时候当您发布一篇日志后，突然发现了一个错误。您可以返回在管理后台，修改这篇日志，但是它却已经在RSS上出现了。有了此技巧，您可以推迟日志出现在RSS的时间，所以您可以放心地仔细检查日志的情况。
打开functions.php，添加下面的代码：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

此代码是增加了10分钟的显示到RSS的延迟时间，您可以修改10这个数字为您所想要延迟的分钟数。
<span class="inner_title">6、在菜单导航里显示特定的类别</span>
<a href="http://www.hopes4.me/images/uploads/2009/08/catmenu.gif"><img style="display: block; float: none; margin-left: auto; margin-right: auto; border: 0px;" title="Display Certain Categories in a Menu" src="http://www.hopes4.me/images/uploads/2009/08/catmenu_thumb.gif" border="0" alt="Display Certain Categories in a Menu" width="484" height="154"></a>
在许多情况下，用户只想在页面的顶部的导航菜单上显示某些特定的分类。那块区域只有有限的空间，只能置放几个比较热门的分类，但如果您使用默认wp_list_categories代码，它将会显示所有的分类。这就是为什么当你想创建一个只显示某些特定分类的导航菜单时，下面的这个技巧就变得非常有用了。


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

请注意，您还可以将“include”改成“exclude”，这样可以显示除了那些你不想显示的以外所有的分类。代码里的数字代表了分类的ID 。请记住，因为WordPress是用清单格式来显示分类，所以您将需要修改CSS来使其正常显示。
<span class="inner_title">7、将引用从评论中独立出来</span>
<a href="http://www.hopes4.me/images/uploads/2009/08/ctseparate.gif"><img style="display: block; float: none; margin-left: auto; margin-right: auto; border: 0px;" title="Separate TrackBacks from Comments" src="http://www.hopes4.me/images/uploads/2009/08/ctseparate_thumb.gif" border="0" alt="Separate TrackBacks from Comments" width="484" height="154"></a>
当您在博客是写了一篇出色的日志后，这篇日志可能被博客圈内地链接。与此同时，这篇出色的日志也可能会引发很多的评论和讨论。如果您没有将引用从评论中独立出来，那样读者就很难继续关注相关的讨论和讨论。下面的这个技巧，可以告诉您如何将引用从评论中独立出来。
首先您需要打开comments.php，并找到看起来像这样的循环：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

替换为：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

上面的代码告诉WordPress将引用和评论分开显示在两个列表。
<span class="inner_title">8、如何列出未来的“即将到来的”日志</span>
<a href="http://www.hopes4.me/images/uploads/2009/08/futureposts.gif"><img style="display: block; float: none; margin-left: auto; margin-right: auto; border: 0px;" title="List Future Scheduled Posts" src="http://www.hopes4.me/images/uploads/2009/08/futureposts_thumb.gif" border="0" alt="List Future Scheduled Posts" width="484" height="154"></a>
每个人都希望有更多的用户订阅其供稿。在您的博客为读者显示未来的日志，是一个可以使读者更感兴奋和兴趣的方式。
首先您需要为未来的日期计划您的日志，然后打开您的sidebar.php或您想要显示的未来日志的清单的地方，粘贴以下代码：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

上面的代码是按参数post_status排序的，目前是按“未来”来排序 ，但它可以是“草稿”，“已发布”或其他等等。另外还存在一个参数限制了日志显示的数量， showposts = 10。您可以更改这个数字，改成您想要显示给您的读者的数量。
<span class="inner_title">9、在每篇日志里显示缩略图</span>
<a href="http://www.hopes4.me/images/uploads/2009/08/thumbnailpost.gif"><img style="display: block; float: none; margin-left: auto; margin-right: auto; border: 0px;" title="Display Thumbnails Next to Each Post" src="http://www.hopes4.me/images/uploads/2009/08/thumbnailpost_thumb.gif" border="0" alt="Display Thumbnails Next to Each Post" width="484" height="154"></a>
一幅图片胜过千言万语。我们都曾经听到过这样的说法，它对博客也同样适用。您不可能通过很短的摘录来很好地说明您的日志，但增加一幅图片却能给日志带来生气，使读者更想点击它。通过自定义字段的技巧，我们将告诉您如何可以做到这一点。
首先，您需要一个大小为210 × 210px的默认图像，就像我们用在WPBeginner上的。您可以命名此预设图片的名称为defaultimage.gif或在这个例子中我们使用的wpbeginner.gif，并确保将图片上传到您的博客主题所在的文件夹中。
然后，您需要打开您的index.php，将以下代码粘贴到您想要的图片显示的地方。


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

<span class="inner_title">10、为您的日志设定到期时间</span>
<a href="http://www.hopes4.me/images/uploads/2009/08/expired.gif"><img style="display: block; float: none; margin-left: auto; margin-right: auto; border: 0px;" title="Set an Expiration Date for Your Posts" src="http://www.hopes4.me/images/uploads/2009/08/expired_thumb.gif" border="0" alt="Set an Expiration Date for Your Posts" width="484" height="154"></a>
当您正在进行一场比赛时，这个技巧会变得非常有用，因为你可能会发布类似线索或暗示之类的信息，但你又不想永远留下它们。您可以使日志自动失效，而不是手动来删除它。另外，当你有一件商品是提供折扣的时候，这个技巧也会变得有用。您张贴折扣在您的博客上，但您并不希望在折扣结束后，它还留在您的博客上。您可以通过下面的代码来自动地删除它。
你所要做的只是将WordPress的循环用下面的代码来代替：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

做完上面的工作后，您就可以通过自定义字段来为日志设定一个过期日间。请确定你使用的关键字是“key”，并且用下面的日间格式：mm/dd/yyyy 00:00:00。
这个技巧其实并不会删除或取消发布您的日志，而只是不会显示在您的博客上。
<span class="inner_title">11、批量删除日志修订版本</span>
<a href="http://www.hopes4.me/images/uploads/2009/08/deleterevision.gif"><img style="display: block; float: none; margin-left: auto; margin-right: auto; border: 0px;" title="Delete Batches of Post Revisions" src="http://www.hopes4.me/images/uploads/2009/08/deleterevision_thumb.gif" border="0" alt="Delete Batches of Post Revisions" width="484" height="154"></a>
WordPress有许多很好的特点，其中之一就是日志修订版本。从WordPress2.6版本后引入此功能，虽然这是一个好的特点，但也会产生一点问题，而问题之一就是会使数据库变得庞大。根据您需要花多少时间来完成一篇日志，您可能会有50多个日志修订版本。您可以手工删除它们，或者您也可以通过现在要介绍给你的，使用一句简单的查询语句来删除这些没用的修订版本。
首先您要做的是登陆到您的phpMyAdmin并选择WordPress数据库。
点击SQL按钮，然后输入下面的查询语句：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

这条查询语句所做的工作是，查询wp_posts表，删除所有post_type字段等于revision的记录。通过这条语句，可以为您节省一部分空间。
<span class="inner_title">12、在您的博客上显示任何RSS种子</span>
<a href="http://www.hopes4.me/images/uploads/2009/08/rsstohtml.gif"><img style="display: block; float: none; margin-left: auto; margin-right: auto; border: 0px;" title="Display Any RSS Feed on Your Blog" src="http://www.hopes4.me/images/uploads/2009/08/rsstohtml_thumb.gif" border="0" alt="Display Any RSS Feed on Your Blog" width="484" height="154"></a>
WordPress有些时候博客主想要在博客上显示关于其他网站的RSS，可能它是一个相关的博客。这时这个技巧就可以起作用了，因为它可以使这一过程变得更简单。有一些脚本和插件可以为您实现这一功能，但我们并不需要它们，因为WordPress内建了这一功能。
所有你需要做的只是将下面的代码复制到您想要RSS的种子被显示的地方，大部分情况下是在sidebar.php中：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

<span class="inner_title">13、一键完成在特定的日志显示“Digg This”按钮</span>
<a href="http://www.hopes4.me/images/uploads/2009/08/diggthis.gif"><img style="display: block; float: none; margin-left: auto; margin-right: auto; border: 0px;" title="Display Digg This Button in Specific Posts" src="http://www.hopes4.me/images/uploads/2009/08/diggthis_thumb.gif" border="0" alt="Display Digg This Button in Specific Posts" width="484" height="154"></a>
日志中的“Digg”按钮非常有用，特别是当日志被提交到Digg。但是您并不需要将“Digg This”按钮放到每篇日志中，因为并不是每篇日志都值得digg。这个技巧会告诉您可以通过自定义字段在特定的日志里显示“Digg This”按钮。
把下面的代码加到single.php中您想要显示的地方：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

现在你可以在创建一篇日志时使用“digg”字段，设置任何值，在日志中显示“Digg This”按钮。如果您不加上这个自定义字段，那按钮就不会显示。简单易用。
<span class="inner_title">14、在某一区域显示置顶日志</span>
<a href="http://www.hopes4.me/images/uploads/2009/08/stickypost.gif"><img style="display: block; float: none; margin-left: auto; margin-right: auto; border: 0px;" title="Display Sticky Posts in One Area" src="http://www.hopes4.me/images/uploads/2009/08/stickypost_thumb.gif" border="0" alt="Display Sticky Posts in One Area" width="484" height="154"></a>
这一功能是很多博客主想要的，因此被包含在WordPress中。现在这个技巧将向展示如何把您所有的置顶日志作为特色日志，显示在主页或其他页面。


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

您可以修改数字5来决定您想要显示多少篇日志在您的页面上，您也可以显示所有的日志，只要把“the_excerpt”改成“the_content”。
<span class="inner_title">15、在第一篇日志后显示广告</span>
在日志后面放上广告真得可以帮你赚到一些钱，因为广告主喜欢这个区域。但是如果您使用普通代码添加广告，那样的话广告会出现每一篇日志后，这样会读者来说是个困扰。通过下面的技巧，您可以仅在第一篇日志后添加广告。
将您的index.php中现在在使用的循环的代码，替换成下面的代码：


{% codeblock %}
function print_post_title() {
global $post;
$thePostID = $post->ID;
$post_id = get_post($thePostID);
$title = $post_id->post_title;
$perm = get_permalink($post_id);
$post_keys = array(); $post_val = array();
$post_keys = get_post_custom_keys($thePostID);

if (!empty($post_keys)) {
foreach ($post_keys as $pkey) {
if ($pkey==’url1′ || $pkey==’title_url’ || $pkey==’url_title’) {
$post_val = get_post_custom_values($pkey);
}
}
if (empty($post_val)) {
$link = $perm;
} else {
$link = $post_val[0];
}
} else {
$link = $perm;
}
echo ‘<h2><a href="’.$link.’" rel="bookmark" title="’.$title.’">’.$title.’</a></h2>’;
}
{% endcodeblock %}

上面的代码会在您第二篇日志后显示广告，请确认你想要把广告放在这个地方。