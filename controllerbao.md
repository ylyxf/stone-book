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

	@RequestMapping("/order/OrderList.do")
	public String list(OrdertForm orderForm,Model model) {
		SimpleCondition condition = new SimpleCondition();
		condition.orderAsc("sortNo");
		List<Order> orderList = service.list(condition);
		model.addAttribute("orderList", orderList);
		return "order/OrderList";
	}

}
```

我们从这里总结一下，Controller类里面的一些命名规则：
