# DNS云服务统一 API

## 安装

```shell
composer require gemini/dns-cloud
```

## 使用

创建配置

```shell
php bin/hyperf.php vendor:publish gemini/dns-cloud
```

设置环境变量

```dotenv
DNS_CLOUD_ALIYUN_ACCESS_KEY_ID="xxx"
DNS_CLOUD_ALIYUN_ACCESS_SECRET="xxx"
```

编写测试代码，我们直接把代码全部写到控制器里，开发者请按照实际情况酌情处理

```php
<?php

declare(strict_types=1);
/**
 * This file is part of Hyperf.
 *
 * @link     https://www.hyperf.io
 * @document https://hyperf.wiki
 * @contact  group@hyperf.io
 * @license  https://github.com/hyperf/hyperf/blob/master/LICENSE
 */

namespace App\Controller;

use AlibabaCloud\SDK\Alidns\V20150109\Alidns;
use AlibabaCloud\SDK\Alidns\V20150109\Models\DescribeDnsProductInstancesRequest;
use AlibabaCloud\Tea\Utils\Utils\RuntimeOptions;
use Gemini\DnsCloud\Factory;
use Hyperf\Di\Annotation\Inject;

class IndexController extends Controller
{
    #[Inject]
    protected Factory $factory;

    public function index()
    {
        /** @var Alidns $client */
        $client = $this->factory->get('aliyun')->client();

        $describeDnsProductInstanceRequest = new DescribeDnsProductInstancesRequest();
        $runtime = new RuntimeOptions([]);

        $res = $client->describeDnsProductInstancesWithOptions($describeDnsProductInstanceRequest, $runtime);

        return $this->response->success($res);
    }
}

```
