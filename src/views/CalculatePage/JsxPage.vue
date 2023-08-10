
<script lang="tsx">
import { defineComponent, ref } from 'vue'
import Portal from '../../Portal.vue'
import Form from './Form.vue'

export default defineComponent({
  setup() {
    const message = ref('Hello, JSX Component!')
    const sampleData = ref([
    { id: 0, name: 'Liam Doe', age: 40, email: 'liam@example.com' },
      { id: 1, name: 'John Doe', age: 30, email: 'john@example.com' },
      { id: 2, name: 'Jane Smith', age: 28, email: 'jane@example.com' },
      { id: 3, name: 'Michael Johnson', age: 35, email: 'michael@example.com' },
      { id: 4, name: 'Emily Brown', age: 25, email: 'emily@example.com' },
      { id: 5, name: 'William Davis', age: 40, email: 'william@example.com' },
      { id: 6, name: 'Olivia Wilson', age: 22, email: 'olivia@example.com' },
      { id: 7, name: 'James Martinez', age: 33, email: 'james@example.com' },
      { id: 8, name: 'Sophia Johnson', age: 29, email: 'sophia@example.com' },
    ]);
    const createData = (name: string, age: number, email: string) => {
      const data = {
        id: sampleData.value.length,
        name,
        age,
        email
      }
      sampleData.value = [...sampleData.value, data]
      setOpen(false)
    }
    const selectedData = ref(sampleData.value[0]);
    const handleSelectedData = (id: number) => {
      selectedData.value = sampleData.value[id % (sampleData.value.length)]
    }
    const open = ref(false); 
    const setOpen = (state: boolean) => {
      open.value = state;
    }

    return {
      message,
      sampleData,
      selectedData,
      handleSelectedData,
      open,
      setOpen,
      createData
    }
  },
  render() {
    return (
      <div>
        <h1>{this.selectedData.name}</h1>
        <button class="button" onClick={() => this.setOpen(true)}> Add Card</button>
        <div class="card-container">
          { this.sampleData.map((data) => {
            return (
              <div class={['card', { 'selected': data.id === this.selectedData.id }]} key={data.id} onClick={() => this.handleSelectedData(data.id)}>
                <div class="card-header">
                  <h2 class="card-title">{data.name}</h2>
                </div>
                <div class="card-body">
                  <slot>age: {data.age}</slot>
                  <slot>email: {data.email}</slot>
                </div>
              </div>
            )
          })}
        </div>
        {this.open && (<Portal>
          <div class="modal-overlay" id="modalOverlay">
            <div class="modal">
              <button class="close-modal-button" onClick={() => this.setOpen(false)}>Cancel</button>
              <Form onSubmit={this.createData} onClose={() => this.setOpen(false)}/>
            </div>
          </div>
          </Portal>)
        }
      </div>
    )
  }
})
</script>

<style scoped>

.card-container {
  display: grid;
  flex-wrap: wrap;
  grid-template-columns: repeat(2, 1fr);
}
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.5);
  justify-content: center;
  align-items: center;
  z-index: 1000;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background-color: rgb(0, 41, 71);
  padding: 20px;
  border-radius: 10px;
  max-width: 90%;
  max-height: 90%;
}

.close-modal-button {
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: rgb(3, 150, 255);
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
  cursor: pointer;
}

.open-modal-button {
  margin: 20px;
  padding: 10px 20px;
  background-color: #007bff;
  border: none;
  border-radius: 5px;
  color: white;
  cursor: pointer;
}

.card {
  border: 1px solid #ccc;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  margin: 10px;
  padding: 10px;
}
.selected {
  outline: 2px solid pink;
}

.card-header {
  background-color: #013957;
  border-bottom: 1px solid #ccc;
  padding: 5px 16px;
  border-radius: 4px 4px 0 0;
}

.card-title {
  margin: 0;
  padding: 0;
  font-size: 1.2em;
}

.card-body {
  padding: 10px 0;
}
</style>
