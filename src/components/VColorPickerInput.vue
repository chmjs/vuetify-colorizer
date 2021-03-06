<template>
  <div class="colorizer-picker-input">
    <v-menu v-model="visible"
            max-width="416px"
            :return-value="color">
      <template v-slot:activator="{ on }">
        <v-text-field readonly
                      outlined
                      hide-details
                      clearable
                      clear-icon="clear"
                      placeholder="Select color"
                      align-center
                      color="primary"
                      :value="colorName"
                      :disabled="disabled"
                      @click:clear="clearColor"
                      v-on="on">
          <template v-slot:label>
            <div>{{ label }}
              <v-tooltip slot="append"
                         top
                         class="help-tooltip">
                <template v-slot:activator="{ on }">
                  <v-btn icon
                         v-on="on"
                         @click.stop>
                    <v-icon class="help-icon material-icons-outlined">info</v-icon>
                  </v-btn>
                </template>
                <span>Help tooltip</span>
              </v-tooltip>
            </div>
          </template>
        </v-text-field>
      </template>
      <VColorPicker :hide-tabs="hideTabs"
                    :value="value"
                    :hex-color="color"
                    :return-type="returnType"
                    @input="setColor" />
    </v-menu>
    <div v-if="color"
         class="color-box-preview"
         :class="color.name"
         :style="colorStyle"
         @click="toggleMenu" />
  </div>
</template>

<script>
import {
  isString,
  isObject,
  isNil,
  startsWith,
} from 'lodash';

import VColorPicker from './VColorPicker';


export default {
  name: 'VColorPickerInput',
  components: {
    VColorPicker,
  },
  props: {
    hideTabs: {
      type: Boolean,
      default: false,
    },
    label: {
      type: String,
      default: 'Color',
    },
    value: {
      type: [Object, String],
      default: null,
    },
    returnType: {
      type: String,
      default: 'color',
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      color: null,
      visible: false,
    };
  },
  computed: {
    colorName() {
      return isObject(this.color) && !isNil(this.color) ? this.color.name : null;
    },
    colorStyle() {
      return {
        backgroundColor: this.color.value,
      };
    },
  },
  watch: {
    value: {
      handler(value) {
        if (isString(value)) {
          if (startsWith(value, '#')) {
            this.setColor({
              value,
            });
          } else {
            this.setColor({
              name: value,
            });
          }
        } else {
          this.setColor(value);
        }
      },
      immediate: true,
    },
  },
  methods: {
    getColorType() {
      if (this.color) {
        return this.color[this.returnType];
      }
      return null;
    },
    setChange() {
      const value = this.returnType === 'color' ? this.color : this.getColorType();
      this.$emit('change', value);
    },
    setColor(value) {
      if (isObject(value)) {
        this.color = value;
      } else {
        let color;
        if (startsWith(value, '#')) {
          color = {
            value,
          };
        } else {
          color = {
            name: value,
          };
        }

        this.color = color;
      }

      this.setChange();
    },
    clearColor() {
      this.color = null;
      this.visible = false;
      this.setChange();
    },
    toggleMenu() {
      this.visible = !this.visible;
    },
  },
};
</script>

<style lang="scss">
.colorizer-picker-input {
  .v-label {
    .v-btn__content {
      height: 14px;
      width: 14px;
    }

    .v-icon {
      font-size: 14px !important;
    }
  }

  .v-btn--icon {
    height: 14px !important;
    width: 14px !important;
    margin: 0 !important;
    color: grey;
  }

  .v-btn--icon {
    pointer-events: all;
  }

  .help-icon {
    color: #7a7a7a !important;
    font-size: 14px;
  }

  .color-box-preview {
    border-radius: 4px;
    position: absolute;
    right: 3em;
    top: 18px;
    width: 20px;
    height: 20px;
    cursor: pointer;
  }
}
</style>
