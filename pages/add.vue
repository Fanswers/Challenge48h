<template>
    <div class="container">
        <div>
            <b-button v-b-modal.modal-1 variant="outline-primary">Ajouter une photo</b-button>
            <b-button variant="outline-primary"><NuxtLink to="list">Liste</NuxtLink></b-button>
            <b-modal id="modal-1" title="Ajouter une image">
              <form action="" @submit.prevent="AddImage">
                <b-form-group id="input-group-2" label="Nom" label-cols-lg="2" required>
                <b-form-input
                  v-model="name"
                  id="input-2"
                  placeholder=""
                  required
                  ></b-form-input>
                </b-form-group>    

            <b-form-group label="Image" label-for="form-image" label-cols-lg="2">
                <b-input-group>
                    <b-form-file id="form-image" :disabled="busy" accept="image/*"></b-form-file>
                </b-input-group>
            </b-form-group>
<b-form-group id="input-group-2" label="Image type" label-cols-lg="2" required>
                <b-form-select v-model="imageType" class="mb-3">
                    <b-form-select-option :value="null" disabled>Please select image type</b-form-select-option>
                    <b-form-select-option value="passionFroid">Passion Froid</b-form-select-option>
                    <b-form-select-option value="fournisseur">Fournisseur</b-form-select-option>
                    <b-form-select-option value="logo">Logo</b-form-select-option>
                </b-form-select>
            </b-form-group>

            <b-form-checkbox v-model="productImage" name="check-button">
              productImage
            </b-form-checkbox>
            <b-form-checkbox v-model="humanImage" name="check-button">
              humanImage
            </b-form-checkbox>
            <b-form-checkbox v-model="institutionalImage" name="check-button">
              institutional Image
            </b-form-checkbox>

            <b-form-group
                v-model="imageFormat"
                label=""
                label-cols-lg="3"
                label-align-sm="right"
                class="mb-2"
                v-slot="{ ariaDescribedby }"
            >
                <b-form-radio-group
                    class="pt-2"
                    :options="['Vertical', 'Horizontal']"
                    :aria-describedby="ariaDescribedby"
                ></b-form-radio-group>
            </b-form-group>

            <b-form-group v-model="imageCredits" id="input-group-2" label="Credits" label-cols-lg="2" class="mt-3" required>
                <b-form-input
                id="input-2"
                placeholder=""
                required
                ></b-form-input>
            </b-form-group>    

            <b-form-checkbox v-model="limitedRightsOfUse" name="check-button">
            Limited rights of use
            </b-form-checkbox>

            <b-form-group v-model="Copyright" id="input-group-2" label="Copyright" label-cols-lg="2" class="mt-3" required>
                <b-form-input
                id="input-2"
                placeholder=""
                required
                ></b-form-input>
            </b-form-group>  
<label for="datepicker-placeholder">Date limite</label>
            <b-form-datepicker v-model="EndDateRightsOfUse" id="datepicker-placeholder" placeholder="Choose a date" locale="en" class=mb-3></b-form-datepicker>

            <label for="tags-basic">Tags</label>
            <b-form-tags 
                input-id="tags-remove-on-delete"
                :input-attrs="{ 'aria-describedby': 'tags-remove-on-delete-help' }"
                v-model="value"
                separator=" "
                placeholder="Ajouter des tags et appuyer sur espace pour confirmer"
                remove-on-delete
                no-add-on-enter
                class="mb-3">
            </b-form-tags>

            <div class="d-flex justify-content-center">
                <b-button type="submit" :disabled="busy">Submit</b-button>
            </div>
            </form>
            </b-modal>
        </div>
    </div>
</template>

<script>
import gql from 'graphql-tag'
export default {
  name: "AddImage",
  data() {
    return {
      name:'',
      productImage:'',
      humanImage: '',
      institutionalImage: '',
      imageCredits: '',
      limitedRightsOfUse:'',
      Copyright: '',
      EndDateOfUse: '',
    }
  },
  methods: {
    AddImage() {
      this.$apollo.mutate({
        mutation: gql`
          mutation(
            $name: String,
            $productImage: Boolean,
            $humanImage: Boolean,
            $institutionalImage: Boolean,
            $imageCredits: String,
            $limitedRightsOfUse: Boolean,
            $Copyright: String,
            $EndDateOfUse: Date,
          ){
          AddImage(
            input:{
              data:{
                name: $name
                productImage: $productImage
                humanImage: $humanImage
                institutionalImage: $institutionalImage
                imageCredits: $imageCredits
                limitedRightsOfUse: $limitedRightsOfUse
                Copyright: $Copyright
                EndDateOfUse : $EndDateOfUse
              }
            })
            {
              produit{
                id
                name
                productImage
                humanImage
                institutionalImage
                imageCredits
                limitedRightsOfUse
                Copyright
                EndDateOfUse
              }}
            }
        `,
        variables: {
          produit: this.produit
        }
      })
      .then((data) => {
        event.target.reset()
      })
    }
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
    </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: ""
    };
  },

  methods: {
    submit() {
      this.$emit("submit", {
        email: this.email,
        password: this.password
      });
    }
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>