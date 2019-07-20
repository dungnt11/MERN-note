# Redux-saga

**Midderware** của redux

## Cách dùng

1. Khi nghe ngóng nhiều hành động

   ```javascript
   export default function* root() {
     yield fork(watchIncrementAsync)
   }
   ```

   

> Ta sử dụng fork để thực hiện các hành động rẽ nhánh

Khi xử lý dạng chờ đợi hành động ta sẽ kết hợp ```while ``` và ``` take``` 

```javascript
export function* nextRedditChange() {
  while (true) {
    const prevReddit = yield select(selectedRedditSelector)
    yield take(actions.SELECT_REDDIT)

    const newReddit = yield select(selectedRedditSelector)
    const postsByReddit = yield select(postsByRedditSelector)
    if (prevReddit !== newReddit && !postsByReddit[newReddit]) yield fork(fetchPosts, newReddit)
  }
}
```

2. Cancel hành động

   Vẫn sử dụng ```fork``` để thực  hiện hành động riêng lẻ

   ```javascript
   export default function* rootSaga() {
     yield fork(watchIncrementAsync)
   }
   ```

   Gọi đến hàm ```watchIncrementAsync``` 

   ```javascript
   export function* watchIncrementAsync() {
     try {
       while (true) {
         const action = yield take(INCREMENT_ASYNC)
         yield race([call(incrementAsync, action), take(CANCEL_INCREMENT_ASYNC)])
       }
     } finally {
       console.log('watchIncrementAsync terminated')
     }
   }
   ```

   > Lưu ý: Sử dụng ```race``` để xem hành động nào diễn ra trước và hoàn thành thì huỷ bỏ, ở đây là ```race``` giữa việc call func ```incrementAsync``` và việc **cancel func** từ người dùng

   **Hàm xử lý login**

   ```javascript
   export function* incrementAsync({ value }) {
     const chan = yield call(countdown, value)
     try {
       while (true) {
         let seconds = yield take(chan)
         yield put({ type: INCREMENT_ASYNC, value: seconds })
         // push liên tục action 
       }
     } finally {
       if (!(yield cancelled())) { // nếu hành động chưa bị huỷ
         yield put(action(INCREMENT)) // push action 
         yield put(action(COUNTDOWN_TERMINATED))
       }
       chan.close() // huỷ việc gọi 
     }
   }
   ```

   