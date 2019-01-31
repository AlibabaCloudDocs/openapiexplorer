# 通过命令行调用API {#concept_74637_zh .concept}

OpenAPI Explorer内置了云命令工具Cloud Shell。Cloud Shell是基于阿里云CLI构建的一款网页版CLI工具，无需安装和配置AccessKey，登录后即可使用。

阿里云云产品的API分为RPC和RESTful两种类型，大部分产品提供RPC API，例如云服务器ECS，云数据库RDS和负载均衡等。

不同类型的API的调用方法也不同。您可以通过以下特点判断API类型：

-   API参数中包含Action字段的是RPC API，需要PathPattern参数的是RESTful API。
-   一般情况下，一个云产品的API类型是一致的。

## 启动Cloud Shell {#section_xcd_g1r_kgb .section}

完成以下操作，在OpenAPI Explorer中启动Cloud Shell：

1.  打开浏览器，输入[https://api.aliyun.com](https://api.aliyun.com)访问OpenAPI Explorer。
2.  在顶部菜单栏，单击**命令行工具集**打开Cloud Shell。
3.  使用阿里云账号登录。

## 在Cloud Shell中调用RPC API {#rpc .section}

在云命令中调用RPC API需遵循以下格式：

```
aliyun <ProductCode> <ActionName> [--parameter1 value1 --paramter2 value2]
```

其中：

-   ProductCode：要调用的云产品 code，比如云服务器的产品code为`ecs`，负载均衡的产品code 为`slb`。您可以执行`aliyun --help`命令查看产品code。
-    ActionName：要调用的 API。比如使用 ECS 的 `DescribeInstanceAttribute` 接口查看一个 ECS 实例的详细信息。
-   parameter：要传入的请求参数。具体参见各产品的API文档。

 **示例** 

在Cloud Shell中执行以下命令，查看指定ECS实例的配置信息。

**说明：** 运行前，请替换实例ID。

```
aliyun ecs DescribeInstanceAttribute --InstanceId i-bp198exxxxxx | jq 
```

## 在Cloud Shell中调用RESTful API {#section_uhy_4cc_kgb .section}

部分阿里云产品如容器服务是RESTful API。RESTful API与RPC API的调用方式不同。使用阿里云CLI调用RESTful API的基本结构如下：

-   **GET请求**

    ```
    aliyun <ProductCode> GET /<Resource>
    ```

    **示例**

    ```
    aliyun cs GET /clusters
    ```

-   **POST请求**

    ```
    aliyun <ProductCode> POST /<Resource> --body "$(cat input.json)"
    ```

    **示例**

    ```
    aliyun cs POST /clusters//attach --header "Content-Type=application/json" --body "$(cat attach.json)"
    ```

-   **DELETE请求**

    ```
    aliyun <ProductCode> DELETE /<Resource>
    ```

    **示例**

    ```
    aliyun cs DELETE /clusters/<cluster-id>
    ```


