<script>
import { defineComponent } from 'vue'

export default defineComponent({
  props: {
    classList: Array
  },
  setup(props)
  {
    return (/* { $props: prop } */) => (
      <div className={`boxWrapper d-flex ${props.classList.join(' ')}`}>
        {Array.from({ length: 10 }).map((item, key) =>
          <div className="boxItem" key={key}>{ key + 1 }</div>
        )}
      </div>
    )
  }
})
</script>
