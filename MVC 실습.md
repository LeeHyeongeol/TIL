# review
사용자가 보는 화면이고 이벤트를 발생시키는 주체다. -> 장바구니에 추가된 상품을 주문하는 이벤트 발생
```jsx
import React from 'react';
import Nav from './components/Nav';
import ItemListContainer from './pages/ItemListContainer';
import NotificationCenter from './components/NotificationCenter';
import './App.css';
import {
  BrowserRouter as Router,
  Switch,
  Route
} from 'react-router-dom';
import ShoppingCart from './pages/ShoppingCart';
import OrderList from './pages/OrderList';

function App () {
  return (
    <Router>
      <Nav />
      <Switch>
        <Route exact path='/'>
          <ItemListContainer />
        </Route>
        <Route path='/shoppingcart'>
          <ShoppingCart />
        </Route>
        <Route path='/orderlist'>
          <OrderList />
        </Route>
      </Switch>
      <NotificationCenter />
    </Router>
  );
}

export default App;
```
# controller
review가 요청한 내용을 전달하는데, 데이터가 필요한 경우 model에 데이터를 요청한다. -> 상품리스트 전체를 확인할 수 있고, 주문내역을 추가하거나 확인할 수 있다.
```jsx
const models = require('../models');

module.exports = {
  items: {
    get: (req, res) => {
      models.items.get((error, result) => {
        if (error) {
          res.status(500).send('Internal Server Error');
        } else {
          res.status(200).json(result);
        }
      });
    },
  },
  orders: {
    get: (req, res) => {
      const userId = req.params.userId;
      console.log(`유저id=${userId}`)
      // TODO: 요청에 따른 적절한 응답을 돌려주는 컨트롤러를 작성하세요.
      if (!userId) {
        res.status(500).send('wrong')
      } else {
        models.orders.get(userId, (error, result) => {
          if (error) {
            res.status(500).send('Internal Server Error');
          } else {
            res.status(200).json(result);
          }
        });
      }
    },
    post: (req, res) => {
      const userId = req.params.userId;
      const { orders, totalPrice } = req.body;
      if (!userId || !orders || !totalPrice) {
        res.status(400).send('wrong userID,order,totalPrice')
      } else {
        models.orders.post(userId, orders, totalPrice, (error, result) => {
          if (error) {
            res.status(500).send('잘못된 주문추가입니다.')
          } else {
            res.status(201).json(result)
          }
        })
      }
    },
  },
};
```
# model
데이터베이스와 연결되어 있고, 요청 받은 정보를 데이터베이스에서 가져온다. -> sql 이용해서 가져오기.

```jsx
const db = require('../db');

module.exports = {
  items: {
    get: (callback) => {
      // TODO: Cmarket의 모든 상품을 가져오는 함수를 작성하세요
      const queryString = `SELECT * FROM items`;

      db.query(queryString, (error, result) => {
        if (error) {
          callback(error, null)
        } else {
          callback(null, result)
        }
      });
    },
  },
  orders: {
    get: (userId, callback) => {
      // TODO: 해당 유저가 작성한 모든 주문을 가져오는 함수를 작성하세요
      const queryString = `SELECT orders.id,orders.created_at,orders.total_price,items.name,items.price,items.image,order_items.order_quantity FROM orders
      LEFT JOIN order_items
      ON orders.id = order_items.order_id
      LEFT JOIN items
      ON order_items.item_id = items.id
      WHERE orders.id = ${userId}`

      db.query(queryString, (error, result) => {
        if (error) {
          callback(error, null)
        } else {
          callback(null, result)
        }
      });
    },
    post: (userId, orders, totalPrice, callback) => {
      // TODO: 해당 유저의 주문 요청을 데이터베이스에 생성하는 함수를 작성하세요

      //우선 orders테이블에 userId, totalPrice를 삽입한다.
      const queryPost = `INSERT INTO orders(user_id, total_price) VAlUES (${userId}, ${totalPrice}) `;

      db.query(queryPost, (error, result) => {
        // 쿼리문을 데이터베이스에 전달하고, 콜백함수를 활용해서 다시 주문번호, itemId, quantity를 데이터베이스에 삽입한다. 
        // 여러 데이터를 한번에 넣을땐 bulk insert를 넣어야 해서 이중 배열 형태로 넣어야 한다. 
        // 주문번호는 result 에 담겨 있는데. 
        // console.log(result)
        // 콘솔로그를 활용해서 어떻게 담겼는지 알수 있습니다. 

        const queryPostOrders = `INSERT INTO order_items (order_id, item_id, order_quantity) VAlUES ?`;
        const params = orders.map((el) => [result.insertId, el.itemId, el.quantity])
        db.query(queryPostOrders, [params], (error, result) => {
          callback(error, result)
        })
      })
    }
  }
}

```

