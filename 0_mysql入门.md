# 0 mysql入门
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

```sql
mysql> select * from vendors;
+---------+----------------+-----------------+-------------+------------+----------+--------------+
| vend_id | vend_name      | vend_address    | vend_city   | vend_state | vend_zip | vend_country |
+---------+----------------+-----------------+-------------+------------+----------+--------------+
|    1001 | Anvils R Us    | 123 Main Street | Southfield  | MI         | 48075    | USA          |
|    1002 | LT Supplies    | 500 Park Street | Anytown     | OH         | 44333    | USA          |
|    1003 | ACME           | 555 High Street | Los Angeles | CA         | 90046    | USA          |
|    1004 | Furball Inc.   | 1000 5th Avenue | New York    | NY         | 11111    | USA          |
|    1005 | Jet Set        | 42 Galaxy Road  | London      | NULL       | N16 6PS  | England      |
|    1006 | Jouets Et Ours | 1 Rue Amusement | Paris       | NULL       | 45678    | France       |
+---------+----------------+-----------------+-------------+------------+----------+--------------+
```

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

```sql
+---------+---------+----------------+------------+----------------------------------------------------------------+
| prod_id | vend_id | prod_name      | prod_price | prod_desc                                                      |
+---------+---------+----------------+------------+----------------------------------------------------------------+
| ANV01   |    1001 | .5 ton anvil   |       5.99 | .5 ton anvil, black, complete with handy hook                  |
| ANV02   |    1001 | 1 ton anvil    |       9.99 | 1 ton anvil, black, complete with handy hook and carrying case |
| ANV03   |    1001 | 2 ton anvil    |      14.99 | 2 ton anvil, black, complete with handy hook and carrying case |
| DTNTR   |    1003 | Detonator      |      13.00 | Detonator (plunger powered), fuses not included                |
| FB      |    1003 | Bird seed      |      10.00 | Large bag (suitable for road runners)                          |
| FC      |    1003 | Carrots        |       2.50 | Carrots (rabbit hunting season only)                           |
| FU1     |    1002 | Fuses          |       3.42 | 1 dozen, extra long                                            |
| JP1000  |    1005 | JetPack 1000   |      35.00 | JetPack 1000, intended for single use                          |
| JP2000  |    1005 | JetPack 2000   |      55.00 | JetPack 2000, multi-use                                        |
| OL1     |    1002 | Oil can        |       8.99 | Oil can, red                                                   |
| SAFE    |    1003 | Safe           |      50.00 | Safe with combination lock                                     |
| SLING   |    1003 | Sling          |       4.49 | Sling, one size fits all                                       |
| TNT1    |    1003 | TNT (1 stick)  |       2.50 | TNT, red, single stick                                         |
| TNT2    |    1003 | TNT (5 sticks) |      10.00 | TNT, red, pack of 10 sticks                                    |
+---------+---------+----------------+------------+----------------------------------------------------------------+
```

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

```sql
+---------+----------------+---------------------+-----------+------------+----------+--------------+--------------+---------------------+
| cust_id | cust_name      | cust_address        | cust_city | cust_state | cust_zip | cust_country | cust_contact | cust_email          |
+---------+----------------+---------------------+-----------+------------+----------+--------------+--------------+---------------------+
|   10001 | Coyote Inc.    | 200 Maple Lane      | Detroit   | MI         | 44444    | USA          | Y Lee        | ylee@coyote.com     |
|   10002 | Mouse House    | 333 Fromage Lane    | Columbus  | OH         | 43333    | USA          | Jerry Mouse  | NULL                |
|   10003 | Wascals        | 1 Sunny Place       | Muncie    | IN         | 42222    | USA          | Jim Jones    | rabbit@wascally.com |
|   10004 | Yosemite Place | 829 Riverside Drive | Phoenix   | AZ         | 88888    | USA          | Y Sam        | sam@yosemite.com    |
|   10005 | E Fudd         | 4545 53rd Street    | Chicago   | IL         | 54545    | USA          | E Fudd       | NULL                |
+---------+----------------+---------------------+-----------+------------+----------+--------------+--------------+---------------------+
```

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

```sql
+-----------+---------------------+---------+
| order_num | order_date          | cust_id |
+-----------+---------------------+---------+
|     20005 | 2005-09-01 00:00:00 |   10001 |
|     20006 | 2005-09-12 00:00:00 |   10003 |
|     20007 | 2005-09-30 00:00:00 |   10004 |
|     20008 | 2005-10-03 00:00:00 |   10005 |
|     20009 | 2005-10-08 00:00:00 |   10001 |
+-----------+---------------------+---------+
```

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

```sql
+-----------+------------+---------+----------+------------+
| order_num | order_item | prod_id | quantity | item_price |
+-----------+------------+---------+----------+------------+
|     20005 |          1 | ANV01   |       10 |       5.99 |
|     20005 |          2 | ANV02   |        3 |       9.99 |
|     20005 |          3 | TNT2    |        5 |      10.00 |
|     20005 |          4 | FB      |        1 |      10.00 |
|     20006 |          1 | JP2000  |        1 |      55.00 |
|     20007 |          1 | TNT2    |      100 |      10.00 |
|     20008 |          1 | FC      |       50 |       2.50 |
|     20009 |          1 | FB      |        1 |      10.00 |
|     20009 |          2 | OL1     |        1 |       8.99 |
|     20009 |          3 | SLING   |        1 |       4.49 |
|     20009 |          4 | ANV03   |        1 |      14.99 |
+-----------+------------+---------+----------+------------+
```

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

```sql
+---------+---------+---------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
| note_id | prod_id | note_date           | note_text                                                                                                                                                 |
+---------+---------+---------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
|     101 | TNT2    | 2005-08-17 00:00:00 | Customer complaint:
Sticks not individually wrapped, too easy to mistakenly detonate all at once.
Recommend individual wrapping.                          |
|     102 | OL1     | 2005-08-18 00:00:00 | Can shipped full, refills not available.
Need to order new can if refill needed.                                                                          |
|     103 | SAFE    | 2005-08-18 00:00:00 | Safe is combination locked, combination not provided with safe.
This is rarely a problem as safes are typically blown up or dropped by customers.         |
|     104 | FC      | 2005-08-19 00:00:00 | Quantity varies, sold by the sack load.
All guaranteed to be bright and orange, and suitable for use as rabbit bait.                                      |
|     105 | TNT2    | 2005-08-20 00:00:00 | Included fuses are short and have been known to detonate too quickly for some customers.
Longer fuses are available (item FU1) and should be recommended. |
|     106 | TNT2    | 2005-08-22 00:00:00 | Matches not included, recommend purchase of matches or detonator (item DTNTR).                                                                            |
|     107 | SAFE    | 2005-08-23 00:00:00 | Please note that no returns will be accepted if safe opened using explosives.                                                                             |
|     108 | ANV01   | 2005-08-25 00:00:00 | Multiple customer returns, anvils failing to drop fast enough or falling backwards on purchaser. Recommend that customer considers using heavier anvils.  |
|     109 | ANV03   | 2005-09-01 00:00:00 | Item is extremely heavy. Designed for dropping, not recommended for use with slings, ropes, pulleys, or tightropes.                                       |
|     110 | FC      | 2005-09-01 00:00:00 | Customer complaint: rabbit has been able to detect trap, food apparently less effective now.                                                              |
|     111 | SLING   | 2005-09-02 00:00:00 | Shipped unassembled, requires common tools (including oversized hammer).                                                                                  |
|     112 | SAFE    | 2005-09-02 00:00:00 | Customer complaint:
Circular hole in safe floor can apparently be easily cut with handsaw.                                                                |
|     113 | ANV01   | 2005-09-05 00:00:00 | Customer complaint:
Not heavy enough to generate flying stars around head of victim. If being purchased for dropping, recommend ANV02 or ANV03 instead.   |
|     114 | SAFE    | 2005-09-07 00:00:00 | Call from individual trapped in safe plummeting to the ground, suggests an escape hatch be added.
Comment forwarded to vendor.                            |
+---------+---------+---------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
```