## Run Django Tests on Change

```shell
find apps/image_to_fpr -name "*.py" | entr foreman n python manage.py test --keepdb  -s apps/image_to_fpr
```

Note: If using vagrant, it won't see the change. Consider using [rmate](https://github.com/textmate/rmate) or [rsub](https://github.com/henrikpersson/rsub)