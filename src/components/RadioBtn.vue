<script>
import { defineComponent } from 'vue'

export default defineComponent({
  props: {
    onChange: Function,
    value: Number,
    name: String,
    list: Array
  },
  setup(props)
  {
    return (/* { $props: prop } */) => (
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
              checked={key === props.value}
              onChange={props.onChange}
              value={key}
            />

            { item.text }
          </label>
        )}
      </div>
    )
  }
})
</script>
