# I: Interface Segregation Principle (ISP)

The Interface Segregation Principle states "that clients should not be forced to implement interfaces they don't use. Instead of one fat interface, many small interfaces are preferred based on groups of methods, each serving one submodule."
We can define it in another way. An interface should be more closely related to the code that uses it than the code that implements it. So the methods on the interface are defined by which methods the client code needs rather than which methods the class implements.
Using ISP, we can create separate interfaces for each operation or requirement rather than having a single class to do the same work.
```
public interface IOrder
 {
          void AddToCart();
          void CCProcess();
 }
 
 public class OnlineOrder : IOrder
 {
           public void AddToCart()
           {
                     //Do Add to Cart
           }
 
           public void CCProcess()
           {
                     //process through credit card
           }
 }
 
 public class OfflineOrder : IOrder
 {
          public void AddToCart()
          {
                   //Do Add to Cart
           }
 
           public void CCProcess()
           {
                    //Not required for Cash/ offline Order
                               throw new NotImplementedException();
           }
 }

public interface IOrder
 {
            void AddToCart();
 }
 
 public interface IOnlineOrder
 {
            void CCProcess();
 }
 
 public class OnlineOrder : IOrder, IOnlineOrder
 {
            public void AddToCart()
            {
                       //Do Add to Cart
            }
 
            public void CCProcess()
            {
                       //process through credit card
            }
 }
 
 public class OfflineOrder : IOrder
 {
            public void AddToCart()
            {
                       //Do Add to Cart
            }
 }
```
