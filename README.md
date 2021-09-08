# Moodleの利用制限のテキストをコース上で表示/非表示するためのHTMLブロック

利用制限を非表示にしたいコースにHTMLブロックを作成し以下のソースを貼り付けて保存する。

```
<button onclick='cusotom_hiderestricted();' class='btn btn-primary hiderestrictedbtn' hidestatus='0'>利用制限を隠す</button>
<script>
function cusotom_hiderestricted(action){
    var btn = document.getElementsByClassName('hiderestrictedbtn');
    if(btn[0].getAttribute('hidestatus') == 0 || action == 'hide'){
        for( var i = 0; i < btn.length; i++  ){
            btn[i].setAttribute('hidestatus','1');
            btn[i].innerHTML = '<span lang="ja" class="multilang">利用制限を表示</span><span lang="en" class="multilang">Show restricted</span>';
            btn[i].classList.remove('btn-primary');
            btn[i].classList.add('btn-info');
            btn[i].setAttribute('hidestatus',1);
        }

        var restrictedelements = document.getElementsByClassName('availabilityinfo isrestricted isfullinfo');
        for( var i = 0; i < restrictedelements.length; i++  ){
            restrictedelements[i].setAttribute('style','display:none');
        }
    }else{
        for( var i = 0; i < btn.length; i++  ){
            btn[i].setAttribute('hidestatus','0');
            btn[i].innerHTML = '<span lang="ja" class="multilang">利用制限を隠す</span><span lang="en" class="multilang">Hide restricted</span>';
            btn[i].classList.remove('btn-info');
            btn[i].classList.add('btn-primary');
            btn[i].setAttribute('hidestatus',0);
        }

        var restrictedelements = document.getElementsByClassName('availabilityinfo isrestricted isfullinfo');
        for( var i = 0; i < restrictedelements.length; i++  ){
            restrictedelements[i].removeAttribute('style');
        }
    }
}

window.onload = function(){
    cusotom_hiderestricted('hide');
}
</script>
```
:::note warn
注意点多言語フィルタがONになっているものとしてボタンの文字列を設定しているので、OFFの場合は書き換えること。
:::
