<script>
import { defineComponent } from 'vue'

export default defineComponent({
  props: {
    itemVal: Array,
    asList: Array,
    fbList: Array
  },
  setup(props)
  {
    const setStyle = item => {
      const { grow, shrink, order } = item

      return {
        flexGrow: grow,
        flexShrink: shrink,
        order
      }
    }

    const setClass = item => {
      const classArr = ['itemSelf']
      const { basis, self } = item

      if (props.fbList[basis] && props.fbList[basis].class) {
        classArr.push(props.fbList[basis].class)
      }
      if (props.asList[self] && props.asList[self].class) {
        classArr.push(props.asList[self].class)
      }

      return classArr.join(' ')
    }

    return (/* { $props: prop } */) => (
      <div className="itemWrapper d-flex flex-wrap">
        {props.itemVal.map((item, key) =>
          <div
            className={setClass(item)}
            style={setStyle(item)}
            key={key}
          >
            { key + 1 }
          </div>
        )}
      </div>
    )
  }
})
</script>
