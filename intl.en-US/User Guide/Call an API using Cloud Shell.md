# Call an API using Cloud Shell {#concept_74637_zh .concept}

Cloud Shell is pre-installed in the OpenAPI Explorer. Cloud Shell is an online CLI tool built on Alibaba Cloud CLI. No need to install and configure AccessKey.

The Alibaba Cloud product APIs are divided into two types, RPC API and RESTful API. Most products use RPC style. The method of calling an API differs from different API types.

You can determine the API type by the following characteristics:

-   If an API requires the `Action` parameter, then the API is the RPC type. If an API requires the`PathPattern` API, then the API is the RESTful type.
-   In general, all APIs in a product are of the same type.
-   Each API only supports one calling method. An error `ApiNotFound` is returned if a wrong method is used.

## Start Cloud Shell {#section_xcd_g1r_kgb .section}

To use Cloud Shell in OpenAPI explorer, follow these steps:

1.  Open a web browser, enter [https://api.aliyun.com](https://api.aliyun.com) to access OpenAPI Explorer.
2.  On the top menu, click **Online Linux Shell**.
3.  Log on to Cloud Shell with your Alibaba Cloud account.

## Call RPC APIs in Cloud Shell {#rpc .section}

Use the following command to call an RPC API:

```
aliyun <ProductCode> <ActionName> [--parameter1 value1 --paramter2 value2]
```

where:

-   ProductCode: The code of the product to call. For example, the product code of ECS is `ecs` and the product code of SLB is`slb`. Run the `aliyun --help` command to obtain product codes.

-    ActionName: The API to call. For example, call the `DescribeInstanceAttribute` API to view the detailed information of an ECS instance.

-   parameter: The parameters of the API. For more information about each parameter, see the API documentation of each product.


 **Example** 

Run the following command to view the detailed information of an ECS instance.

**Note:** Change the ID of the ECS instance that you want to view before run the command.

```
aliyun ecs DescribeInstanceAttribute --InstanceId i-bp198exxxxxx | jq 
```

## Call RESTful APIs in the Cloud Shell {#section_uhy_4cc_kgb .section}

Some Alibaba Cloud products, such as Container Service, provide RESTful APIs. The calling method of RESTful APIs is different from that of RPC APIs. The request structure is as follows when calling RESTful APIs in the Cloud Shell:

-   **GET method**

    ```
    aliyun <ProductCode> GET /<Resource>
    ```

    **Example**

    ```
    aliyun cs GET /clusters
    ```

-   **POST method**

    ```
    aliyun <ProductCode> POST /<Resource> --body "$(cat input.json)"
    ```

    **Example**

    ```
    aliyun cs POST /clusters//attach --header "Content-Type=application/json" --body "$(cat attach.json)"
    ```

-   **DELETE method**

    ```
    aliyun <ProductCode> DELETE /<Resource>
    ```

    **Example**

    ```
    aliyun cs DELETE /clusters/<cluster-id>
    ```


