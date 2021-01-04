<template>
  <div>
    <div class="row justify-center">
      <span>Teste do deploy automatizado</span>
      <div class="col-12 q-mt-md row justify-center">
        <VueSignaturePad
          id="signature"
          width="95%"
          height="300px"
          ref="signaturePad"
          :images="imgs"
          :options="options"
        />
      </div>
    </div>
    <div class="q-mt-md">
      <div class="row q-gutter-md justify-center">
        <q-btn class="col-2" outline icon="restore" @click="undo"/>
        <q-btn class="col-2" outline icon="save_alt" @click="save" />
        <q-btn class="col-2" outline label="Color picker" icon="color_lens">
          <q-menu>
            <q-color v-model="hex" />
          </q-menu>
        </q-btn>
        <q-btn
          class="col-2"
          text-color="red"
          unelevated
          icon="delete"
          label="Delete all"
          @click="imgs = []"
        />
      </div>
    </div>
    <div class="q-mt-md">
      <div class="row q-gutter-md justify-center" v-for="(img, key) in imgs" :key="key">
        <img style="border: thin silver solid;" :src="img">
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'MySignaturePad',
  computed: {
    options: function () {
      return {
        penColor: this.hex
      }
    }
  },
  data () {
    return {
      imgs: [],
      hex: '#000'
    }
  },
  methods: {
    undo () {
      this.$refs.signaturePad.undoSignature()
    },
    save () {
      const { isEmpty, data } = this.$refs.signaturePad.saveSignature()
      this.$refs.signaturePad.clearSignature()

      console.log(isEmpty)
      console.log(data)
      this.imgs.push(data)
    }
  }
}
</script>

<style>
#signature {
  border: double 3px transparent;
  border-radius: 5px;
  background-image: linear-gradient(white, white),
    radial-gradient(circle at top left, #4bc5e8, #9f6274);
  background-origin: border-box;
  background-clip: content-box, border-box;
}
</style>
