<script lang="jsx" setup>
import { defineProps, getCurrentInstance } from 'vue'

const props = defineProps({
  onChange: Function,
  value: Number,
  name: String,
  list: Array
})

const _self = getCurrentInstance()

_self.render = () => (
  <div className="radioBox">
    {!!props.list.length && props.list.map((item, key) =>
      <label
        className={key === props.value ? 'checked' : ''}
        htmlFor={`${props.name}_${key}`}
        key={key}
      >
        <input
          type="radio"
          name={props.name}
          id={`${props.name}_${key}`}
          value={key}
          checked={key === props.value}
          onChange={props.onChange}
        />

        { item.text }
      </label>
    )}
  </div>
)
</script>
