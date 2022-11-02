---
title: PHP + ipsw.me API 简陋的 iOS 固件下载
author: Q
type: post
date: 2018-04-09T12:02:09+00:00
url: /blog/942
i3geek_xzh_submit:
  - 1
wp_player_music_type:
  - netease
mp3_xiami_type:
  - song
wp_player_lyric_open:
  - close
ampforwp-amp-on-off:
  - default
views:
  - 2745
categories:
  - iOS
  - Wordpress
tags:
  - API
  - Apple
  - iOS
  - ipsw
  - ipsw.me
  - PHP
  - WordPress

---
  * 无聊写了一个 iOS 固件下载页面 <https://xingxiang.me/ipsw>
  * 用了 ipsw.me 的 API
	
```php
		<h3>1.请选择要下载的产品</h3>
		<p>
			<a href="platform?product=iPhone">iPhone</a><br>
    		<a href="platform?product=iPad">iPad</a><br>
    		<a href="platform?product=Apple TV">Apple TV</a><br>
		</p>
```

```php
<h3>2.请选择要下载的型号</h3>
		<p>
		<?php
$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, "https://api.ipsw.me/v4/devices");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, TRUE);
curl_setopt($ch, CURLOPT_HEADER, FALSE);

curl_setopt($ch, CURLOPT_HTTPHEADER, array(
    "Accept: application/json"
));

$response = curl_exec($ch);
curl_close($ch);

$devices = json_decode($response, true);





$product = $_GET["product"];

foreach (array_reverse($devices) as $device){
    if(strpos($device['name'],$product) !== false){
        echo '<a href="version?identifier='.$device['identifier'].'">'.$device['name'].'</a></br>';
    }
}

?>
</p>
```

```php
<h3>3.请选择要下载的版本</h3>
		<?php
$identifier = $_GET["identifier"];
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.ipsw.me/v4/device/{$identifier}");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, TRUE);
curl_setopt($ch, CURLOPT_HEADER, FALSE);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
  "Accept: application/json"
));
$response = curl_exec($ch);
curl_close($ch);
$versions = json_decode($response,true);
$firmwares = $versions['firmwares'];
?>
<table>
    <tr>
        <th>版本</th>
        <th>签名状态</th>
        <th>发布日期</th>
        <th>MD5</th>
        <th>SHA1</th>
        <th>下载链接</th>
    </tr>
    <?php
    foreach ($firmwares as $firmware){
        $status = $firmware['signed'] == true ? 'Signed' : 'Unsigned';
        $date = substr($firmware['releasedate'], 0, 10);
        echo '<tr><td>'.$firmware['version'].'('.$firmware['buildid'].')</td>
                  <td>'.$status.'</td>
                  <td>'.$date.'</td>
                  <td>'.$firmware['md5sum'].'</td>
                  <td>'.$firmware['sha1sum'].'</td>
                  <td><a href="'.$firmware['url'].'}">下载</a></td>
              </tr>';
        
    }
    ?>
```

```php
		<h3>2.请选择要下载的版本</h3>
		<p>
		<?php
$platform = $_GET['platform'];
$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, "https://api.ipsw.me/v4/itunes/{$platform}");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, TRUE);
curl_setopt($ch, CURLOPT_HEADER, FALSE);

curl_setopt($ch, CURLOPT_HTTPHEADER, array(
  "Accept: application/json"
));

$response = curl_exec($ch);
curl_close($ch);

$versions = json_decode($response,true);
?>

<?php
if ($platform == 'windows'){
    echo '
    <table>
        <tr>
            <th>版本</th>
            <th>发布日期</th>
            <th>32 Bit</th>
            <th>64 Bit</th>
        </tr>';

    foreach ($versions as $version){
        $date = substr($version['releasedate'], 0, 10);
        echo '<tr><td>'.$version['version'].'</td>
              <td>'.$date.'</td>
              <td><a href="'.$version['url'].'">下载</a></td>
              <td><a href="'.$version['64biturl'].'">下载</a></td>
          </tr>';
    }
    echo '</table>';
}else{
    echo '
    <table>
        <tr>
            <th>版本</th>
            <th>发布日期</th>
            <th>下载</th>
        </tr>';

    foreach ($versions as $version){
        $date = substr($version['releasedate'], 0, 10);
        echo '<tr><td>'.$version['version'].'</td>
              <td>'.$date.'</td> 
              <td><a href="'.$version['url'].'">下载</a></td>
          </tr><br>';
}
    echo '</table>';
}

?>
		</p>
```