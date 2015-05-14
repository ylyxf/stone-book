# controller包

controller包也包含两种java类：第一种是Form类,第二种是SpringMVC的Controller类。

Form类：一般情况下，model包的类已经足够为Controller类接收参数所用，但也有不够用的情况，此时需要从model来继承一个Form，给Controller来接收参数。

举个例子：前端要按订单日期查询，用户输入起、止日期，系统返回在这个日期范围内的订单。Controller要接收开始日期、结束日期两个条件，但是Order类中只有一个创建日期字段。这个时候，就需要建立一个Form，来接收前端的参数。

```
    public OrderForm extends Order {

        public Date createDateBegin;

        public Date createDateEnd;

    }
```

再举个Controller类的例子：

```
@Controller
public class OrderController {

	@Autowired
	OrderService service;

	@Autowired
	ClientService clientService;

	@RequestMapping("/order/OrderList.do")
	public String list() {
		return "order/OrderList";
	}

	@RequestMapping("/order/OrderListData.do")
	@ResponseBody
	public List<Order> listData(OrdertForm orderForm) {
		SimpleCondition condition = new SimpleCondition();
		condition.orderAsc("sortNo");
		List<Order> orderList = service.list(condition);
		return orderList;
	}

}
```

我们从这里总结一下，Controller类里面的一些命名规则：
1. Controller类层面上，不写@RequestMapping注解。越到表现层，变数的东西就越多，就越不能有公用的东西。
2. @AutoWired的Service成员变量，如果是本模块的，就直接写service，属于本家，不必啰嗦。如果是其它模块的，如本例的ClientService，变量名则应该写全。
3. url路径的前面部分其实对应着webapp的目录，都小些；url路径的最后部分，对应的是webapp目录下的文件，这个要按驼峰写法命名。如本例的/order就是webapp目录下的order文件夹，/OrderList.do对应的其实是OrderList.jsp文件。
4. url的特殊情况，返回的是json数据，那么前面的目录一样都是小写，最后的部分用首字母小写的驼峰格式来表示。而且一般和对应的页面录径名一致，最后加个Data后缀。如上文加载了OrderList.jsp页面，后面从OrderList.jsp页面上发起请求OrderList的json数据，则其路径应命名为：/order/OrderListData.do
