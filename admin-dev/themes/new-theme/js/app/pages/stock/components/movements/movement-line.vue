<!--**
 * 2007-2017 PrestaShop
 *
 * NOTICE OF LICENSE
 *
 * This source file is subject to the Open Software License (OSL 3.0)
 * that is bundled with this package in the file LICENSE.txt.
 * It is also available through the world-wide-web at this URL:
 * https://opensource.org/licenses/OSL-3.0
 * If you did not receive a copy of the license and are unable to
 * obtain it through the world-wide-web, please send an email
 * to license@prestashop.com so we can send you a copy immediately.
 *
 * DISCLAIMER
 *
 * Do not edit or add to this file if you wish to upgrade PrestaShop to newer
 * versions in the future. If you wish to customize PrestaShop for your
 * needs please refer to http://www.prestashop.com for more information.
 *
 * @author    PrestaShop SA <contact@prestashop.com>
 * @copyright 2007-2017 PrestaShop SA
 * @license   https://opensource.org/licenses/OSL-3.0 Open Software License (OSL 3.0)
 * International Registered Trademark & Property of PrestaShop SA
 *-->
<template>
  <tr>
    <td class="d-flex align-items-center">
      <PSMedia
        class="d-flex align-items-center"
        :thumbnail="thumbnail"
      >
        <p>
          {{ product.product_name }}
          <small v-if="hasCombination"><br />
            {{ combinationName }}
          </small>
        </p>
      </PSMedia>
    </td>
    <td>
      {{ product.product_reference }}
    </td>
    <td>
      <a v-if="orderLink" :href="orderLink" target="_blank">
        {{ product.movement_reason }}
      </a>
      <span v-else>{{ product.movement_reason }}</span>
    </td>
    <td class="text-sm-center">
      <span class="qty-number" :class="{'is-positive' : isPositive}">
        <span v-if="isPositive">+</span>
        <span v-else>-</span>
        {{ qty }}
      </span>
    </td>
    <td class="text-sm-center">
      {{ product.date_add }}
    </td>
    <td>
      {{ employeeName }}
    </td>
  </tr>
</template>

<script>
  import PSMedia from 'app/widgets/ps-media';
  import productDesc from 'app/pages/stock/mixins/product-desc';

  export default {
    props: ['product'],
    mixins: [productDesc],
    computed: {
      qty() {
        return this.product.physical_quantity;
      },
      employeeName() {
        return `${this.product.employee_firstname} ${this.product.employee_lastname}`;
      },
      isPositive() {
        return this.product.sign > 0;
      },
      orderLink() {
        return this.product.order_link !== 'N/A' ? this.product.order_link : null;
      },
    },
    components: {
      PSMedia,
    },
  };
</script>

<style lang="sass" scoped>
  @import "../../../../../../scss/config/_settings.scss";
  .qty-number {
    padding: 2px 5px;
    background-color: $gray-dark;
    display: inline-block;
    min-width: 50px;
    color: white;
    &.is-positive {
      background-color: $brand-primary;
    }
  }
</style>
