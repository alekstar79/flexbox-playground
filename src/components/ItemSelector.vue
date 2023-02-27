<script lang="jsx" setup>
import { defineProps, getCurrentInstance } from 'vue'

const props = defineProps({
  setItemVal: Function,
  number: Number,
  params: Object,
  asList: Array,
  fbList: Array
})

const NumberBox = (attr, data) => (
  <div className="numberBox">
    <div className="roundBtn minusBtn" onClick={() => props.setItemVal(attr, data - 1)}>-</div>
    <div className="number">{ data }</div>
    <div className="roundBtn plusBtn" onClick={() => props.setItemVal(attr, data + 1)}>+</div>
  </div>
)

const _self = getCurrentInstance()

_self.render = () => (
  <div className="selector">
    <div className="text-center font-weight-bold">{ props.number }</div>
    <div className="selRow">
      <span className="selTitle">flex-grow</span>
      {NumberBox('grow', props.params.grow)}
    </div>

    <div className="selRow">
      <span className="selTitle">flex-shrink</span>
      {NumberBox('shrink', props.params.shrink)}
    </div>

    <div className="selRow">
      <span className="selTitle">flex-basis</span>
      <select value={ props.params.basis } onChange={(e) => props.setItemVal('basis', e.target.value)}>
        {props.fbList.map((item, key) => <option value={key} key={key}>{item.text}</option>)}
      </select>
    </div>

    <div className="selRow">
      <span className="selTitle">order</span>
      {NumberBox('order', props.params.order)}
    </div>

    <div className="selRow">
      <span className="selTitle">align-self</span>
      <select value={props.params.self} onChange={(e) => props.setItemVal('self', e.target.value)}>
        {props.asList.map((item, key) => <option value={key} key={key}>{item.text}</option>)}
      </select>
    </div>
  </div>
)
</script>
