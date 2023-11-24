# mysql入门
## 0.1 样例表
这些表主要完成的任务:
1. 管理供应商
2. 管理产品目录
3. 管理顾客列表
4. 录入顾客订单

### vendors表
vendors表存储销售产品的供应商
<table>
    <th>
        <tr><td>列</td><td>说明</td></tr>
    </th>
    <tr><td>vend_id</td><td>唯一的供应商id</td></tr>
    <tr><td>vend_name</td><td>供应商名</td></tr>
    <tr><td>vend_address</td><td>供应商的地址</td></tr>
    <tr><td>vend_city</td><td>供应商的城市</td></tr>
    <tr><td>vend_state</td><td>供应商的州</td></tr>
    <tr><td>vend_zip</td><td>供应商的邮政编码</td></tr>
    <tr><td>vend_country</td><td>供应商的国家</td></tr>
</table>

### products表
products表包含产品目录，每行一个产品。每个产品有唯一的ID
（prod_id列），通过vend_id（供应商的唯一ID）关联到它的供应商。
<table>
    <th>
        <tr><td>列</td><td>说明</td></tr>
    </th>
    <tr><td>prod_id</td><td>唯一的产品ID</td></tr>
    <tr><td>vend_id</td><td>产品供应商ID（关联到vendors表中的vend_id）</td></tr>
    <tr><td>prod_name</td><td>产品名</td></tr>
    <tr><td>prod_price</td><td>产品价格</td></tr>
    <tr><td>prod_desc</td><td>产品描述</td></tr>
</table>

### customers表
customers表存储所有顾客的信息。
<table>
    <th>
        <tr><td>列</td><td>说明</td></tr>
    </th>
    <tr><td>cust_id</td><td>唯一的顾客ID</td></tr>
    <tr><td>cust_name</td><td>顾客名</td></tr>
    <tr><td>cust_address</td><td>顾客的地址</td></tr>
    <tr><td>cust_state</td><td>顾客的州</td></tr>
    <tr><td>cust_zip</td><td>顾客的邮政编码</td></tr>
    <tr><td>cust_country</td><td>顾客的国家</td></tr>
    <tr><td>cust_contact</td><td>顾客的联系名</td></tr>
    <tr><td>cust_email</td><td>顾客的联系email地址</td></tr>
</table>

### orders表
orders表存储顾客订单（但不是订单细节）。
<table>
    <th>
        <tr><td>列</td><td>说明</td></tr>
    </th>
    <tr><td>order_num</td><td>唯一订单号</td></tr>
    <tr><td>order_date</td><td>订单日期</td></tr>
    <tr><td>cust_id</td><td>订单顾客 ID （关系到 customers 表 的
cust_id）</td></tr>
</table>

### orderitems表
orderitems表存储每个订单中的实际物品。
<table>
    <th>
        <tr><td>列</td><td>说明</td></tr>
    </th>
    <tr><td>order_num</td><td>订单号（关联到orders表的order_num）</td></tr>
    <tr><td>order_item</td><td>订单物品号（在某个订单中的顺序）</td></tr>
    <tr><td>prod_id</td><td>产品ID（关联到products表的prod_id）</td></tr>
    <tr><td>quantity</td><td>物品数量</td></tr>
    <tr><td>item_price</td><td>物品价格</td></tr>
</table>

### productnotes表
productnotes表存储与特定产品有关的注释。
<table>
    <th>
        <tr><td>列</td><td>说明</td></tr>
    </th>
    <tr><td>note_id</td><td>唯一注释ID</td></tr>
    <tr><td>prod_id</td><td>产品ID（对应于products表中的prod_id）</td></tr>
    <tr><td>note_date</td><td>增加注释的日期</td></tr>
    <tr><td>note_text</td><td>注释文本</td></tr>
</table>

