# API Spec

Local:
`POST /api/text2pose/` 

Public:
`POST https://pub.cl.uzh.ch/demo/text2pose/`

requests

```
{
    "language_code": "dsgs", # dsgs, lsf-ch, lis-ch
    "text": "In Baar gibt es eine Höhle.",
}
```

returns

```
{
    "language_code": "dsgs", # dsgs, lsf-ch, lis-ch
    "text": "In Baar gibt es eine Höhle.",
    "pose": "..."
}
```

<!-- where `pose` is a JSON string encoded by [jsonpickle](https://jsonpickle.github.io/). To decode, use the `jsonpickle.decode` method and a [Pose](https://github.com/sign-language-processing/pose) object will be recovered. -->

where `pose` is a string encoded by [base64](https://docs.python.org/3/library/base64.html#base64.b64encode). To decode, use the `base64.b64decode` method, then read the decoded bytes into a [Pose](https://github.com/sign-language-processing/pose) object:

```
import base64
import json

from pose_format import Pose


data = json.loads(response.text)
decoded = base64.b64decode(data['pose'])
pose = Pose.read(decoded)
```

To test the API by `cURL`:

```
curl --location 'https://pub.cl.uzh.ch/demo/text2pose/' \
--header 'Content-Type: application/json' \
--data '{
    "text": "In Baar gibt es eine Höhle.",
    "language_code": "dsgs"
}'
```
