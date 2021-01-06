
<script>
import { get, debounce, set } from 'loadsh';
//在抽象组件的生命周期过程中，我们可以对包裹的子组件监听的事件进行拦截，也可以对子组件进行 Dom 操作，
//从而可以对我们需要的功能进行封装，而不需要关心子组件的具体实现。
export default {
  name: 'debounce',
  abstract: true, //标记为抽象组件
  props: {
    events: String,
    wait: {
      type: Number,
      default: 0
    },
    options: {
      type: Object,
      default () {
        return {};
      }
    }
  },
  render () {
    let vnode = this.$slots.default[0]; // 子组件的vnode
    if (vnode && this.events) {
      let eventList = this.events.split(',');
      eventList.forEach(eventName => {
        // vnode.componentOptions.listeners[eventName].forEach((item, index) => {
        //   //vnode.componentOptions.listeners[eventName][index] = debounce(item, 2000, this.options)
        //   set(vnode, `componentOptions.listeners[${eventName}][${index}]`, debounce(item, this.wait, this.options));
        // })
        let event = get(vnode, `data.on[${eventName}]`); // 子组件绑定的click事件
        if (typeof event === 'function') {
          /**
           * 加上debounce操作, 参数与 lodash 的debounce完全相同
           */
          set(vnode, `data.on[${eventName}]`, debounce(event, this.wait, this.options));
        }
      });
    }
    return vnode;
  }
};
</script>