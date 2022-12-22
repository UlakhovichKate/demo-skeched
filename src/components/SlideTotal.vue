<script>
export default {
  props: ['selectedComposition', 'selectedVariations', 'addMessage'],
  data() {
    return {
      messagePrice: 0.50,
      petsPrice: 2,
      fullSum: 0,
    }
  },
  methods: {
    countSum() {
      let messagePrice = this.addMessage.length > 0 ? this.messagePrice : 0;
      this.fullSum = messagePrice + this.petsPrice;

      this.selectedVariations.forEach(item => {
        this.fullSum += item.price * item.count;
      });

      return this.fullSum;
    },
    checkLength() {
      return this.addMessage.length > 0
    },
    checkPrice(el) {
      return el.count > 0
    }
  }
}
</script>

<template>
  <div class="total">
    <div class="total__preview"></div>

    <h2 class="total__title">Total</h2>

    <div class="total__prices">
      <ul class="total__list">
        <li class="total__item"><span class="total__name">{{ selectedComposition.name }}</span> <span class="total__price">£ {{ selectedComposition.price }}</span> </li>
        <li class="total__item" v-for="item in selectedVariations"><span class="total__name" v-if="checkPrice(item)">Card type: {{item.name}} x {{item.count}}</span><span class="total__price" v-if="checkPrice(item)">£ {{item.price * item.count}}</span></li>
        <li class="total__item"><span class="total__name">Pets</span> <span class="total__price">£ {{ petsPrice }}</span> </li>
        <li class="total__item" v-if="checkLength()"><span class="total__name">Message</span> <span class="total__price">£ {{ messagePrice }}</span> </li>
        <li class="total__item--message" v-if="checkLength()"><span class="total__name">Message text:</span><em>{{ addMessage }}</em></li>
      </ul>
    </div>

    <div class="total__final">
      <span class="total__text">final price included V.A.T</span><span class="total__summary"> £ {{ countSum() }}</span>
    </div>

    <button class="total__btn" type="submit">ADD TO CART</button>

    <div class="total__delivery">
      <h3 class="total__subtitle">Delivery</h3>
      <div class="total__delivery-information">
        <span><i class="c-icon" data-fa-i2svg=""><svg class="svg-inline--fa fa-message" aria-hidden="true" focusable="false" data-prefix="far" data-icon="message" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" data-fa-i2svg=""><path fill="currentColor" d="M447.1 0h-384c-35.25 0-64 28.75-64 63.1v287.1c0 35.25 28.75 63.1 64 63.1h96v83.98c0 9.836 11.02 15.55 19.12 9.7l124.9-93.68h144c35.25 0 64-28.75 64-63.1V63.1C511.1 28.75 483.2 0 447.1 0zM464 352c0 8.75-7.25 16-16 16h-160l-80 60v-60H64c-8.75 0-16-7.25-16-16V64c0-8.75 7.25-16 16-16h384c8.75 0 16 7.25 16 16V352z"></path></svg></i></span>
        <p>If you would like us to send directly to the final recipient, tick the box above and we will pop the card in an envelope to them. If you would like to write your own message, leave this unticked and we will send the card to you with an envelop to address and send on.</p>
      </div>
      <div class="total__delivery-information">
        <span><i class="c-icon" data-fa-i2svg=""><svg class="svg-inline--fa fa-heart" aria-hidden="true" focusable="false" data-prefix="fas" data-icon="heart" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" data-fa-i2svg=""><path fill="currentColor" d="M0 190.9V185.1C0 115.2 50.52 55.58 119.4 44.1C164.1 36.51 211.4 51.37 244 84.02L256 96L267.1 84.02C300.6 51.37 347 36.51 392.6 44.1C461.5 55.58 512 115.2 512 185.1V190.9C512 232.4 494.8 272.1 464.4 300.4L283.7 469.1C276.2 476.1 266.3 480 256 480C245.7 480 235.8 476.1 228.3 469.1L47.59 300.4C17.23 272.1 .0003 232.4 .0003 190.9L0 190.9z"></path></svg></i></span>
        <p>We post all items Royal Mail and your delivery will be with you in 7 working days.</p>
      </div>
    </div>
  </div>
</template>

<style>
  .total__preview {
    width: 226px;
    height: 341px;
    margin: auto;
    background: #FFFFFF;
    box-shadow: 0 8px 14px rgba(59, 73, 125, 0.1);
    border-radius: 4px;
  }

  .total__title {
    margin-top: 20px;
    font-family: 'Hatton';
    font-size: 24px;
    line-height: 30px;
    text-align: center;
    text-transform: uppercase;
  }

  .total__prices {
    margin: 20px 0;
    padding-bottom: 30px;
    border-bottom: 1px solid #FFBD9B;
  }

  .total__delivery {
    margin-top: 50px;
    padding: 0 15px;
    text-align: left;
    font-family: 'Hatton';
  }

  .total__list {
    list-style: none;
    padding: 0;
    text-align: left;
  }

  .total__item {
    display: grid;
    grid-template-columns: 1fr 100px;
    font-family: 'Roboto';
  }

  .total__name {
    padding-right: 15px;
    font-weight: 400;
    font-size: 12px;
    line-height: 20px;
  }

  .total__price {
    font-weight: 500;
    font-size: 14px;
    line-height: 24px;
    color: #99715D;
  }

  .total__final {
    display: grid;
    grid-template-columns: 1fr 100px;
    font-family: 'Roboto';
    text-align: left;
  }

  .total__text {
    font-style: italic;
    font-weight: 400;
    font-size: 12px;
    line-height: 24px;
  }

  .total__summary {
    font-weight: 700;
    font-size: 20px;
    line-height: 25px;
  }

  .total__subtitle {
    font-weight: 400;
    font-size: 24px;
    line-height: 30px;
    padding-bottom: 20px;
    text-transform: uppercase;
  }

  .total__delivery-information {
    grid-gap: 12px;
    color: #ababab;
    display: grid;
    font-size: 18px;
    grid-template-columns: 18px 1fr;
    margin-bottom: 18px;
  }

  .total__delivery-information p {
    color: #000;
    font-size: 14px;
    line-height: 1.2;
    padding-bottom: 6px;
  }

  .total__delivery-information .c-icon path {
    fill: #ffbd9b;
  }

  .total__btn {
    margin: 36px auto;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    padding: 19px 25px;
    gap: 20px;
    width: 343px;
    height: 50px;
    background: #000000;
    border-radius: 25px;
    font-family: 'Roboto';
    font-size: 11px;
    line-height: 12px;
    text-align: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;
    color: #FFE5D7;
    cursor: pointer;
  }

  .total__btn:hover {
    opacity: 0.7;
  }
</style>
