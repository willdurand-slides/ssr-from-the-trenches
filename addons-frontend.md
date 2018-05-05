# addons.mozilla.org

Some lessons learnt.


## Double render is a fragile hack, do not use it 😅


## Always be careful

Undefined reference on the server == Error 500.


## Security considerations

- State serialization
- Sensitive data on the server


## Error handling


## Debugging made ~~easy~~ complex

- Isomorphic logging layer but no dev tools
- `disableSSR` config option to the rescue


## New fun bugs...

![](images/new-bug-back.png)


![](images/new-bug-back.gif)


## Fresh, isolated server context

![](images/locale-leak.png)

```shell
$ repeat 10 curl https://addons.mozilla.org/en-US/firefox/addon/adblock-plus/ -s \
  | grep --color -oE 'updated</dt><dd data-reactid=\"\d+\">.+?</dd>'

updated</dt><dd data-reactid="194">il y a 2 jours (6 nov. 2017)</dd>
updated</dt><dd data-reactid="194">2 days ago (Nov 6, 2017)</dd>
updated</dt><dd data-reactid="194">2 days ago (Nov 6, 2017)</dd>
updated</dt><dd data-reactid="194">2 hari yang lalu (6 Nov 2017)</dd>
updated</dt><dd data-reactid="194">2 days ago (Nov 6, 2017)</dd>
updated</dt><dd data-reactid="194">2 days ago (6 Nov 2017)</dd>
updated</dt><dd data-reactid="194">2 dias atrás (6 de nov de 2017)</dd>
updated</dt><dd data-reactid="194">2 days ago (Nov 6, 2017)</dd>
updated</dt><dd data-reactid="194">2 天前 (2017年11月6日)</dd>
updated</dt><dd data-reactid="194">2 days ago (Nov 6, 2017)</dd>
```


## React has useful dev warnings


## No random allowed

![](images/page-stuck.png)
