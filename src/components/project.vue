<template>
  <div class="project"></div>
</template>

<script>
export default {
  name: 'project',
  data() {
    return {
      content: [
        {
          id: 0,
          headerText: 'Сказочное заморское яство',
          name: 'Нямушка',
          component: 'с фуа-гра',
          list: [
            '10 порций',
            'мышь в подарок'
          ],
          weight: '0,5',
          unit: 'кг',
          cardFooter: 'Печень утки разварная с артишоками.'
        },
        {
          id: 1,
          headerText: 'Сказочное заморское яство',
          name: 'Нямушка',
          component: 'с рыбой',
          list: [
            '40 порций',
            '2 мыши в подарок'
          ],
          weight: 2,
          unit: 'кг',
          cardFooter: 'Головы щучьи с чесноком да свежайшая сёмгушка.'
        },
        {
          id: 2,
          headerText: 'Сказочное заморское яство',
          name: 'Нямушка',
          component: 'с курой',
          list: [
            '100 порций',
            '5 мышей в подарок',
            'заказчик доволен'
          ],
          weight: 5,
          unit: 'кг',
          cardFooter: 'Филе из цыплят с трюфелями в бульоне.'
        },
      ],
      imgCat: 'cat.png',
      cardFooter: {
        'default': 'чего сидишь? Порадуй котэ, <span class="bdushed"><button class="btn">купи</button></span>',
        'disabled': 'Печень утки разварная с артишоками.'
      }
    }
  },
  methods: {
    init(selector) {
      
      let app = document.querySelector(selector);
      let question = `<div class="question">Ты сегодня покормил кота?</div>`;
      let cards = `<div class="cards"></div>`;

      app.insertAdjacentHTML('afterbegin', question);
      app.insertAdjacentHTML('beforeend', cards);

      this.createCard();

      this.listener();
      
    },
    createCard() {
      if (this.content.length > 0) {

        for (let i=0; i<this.content.length; i++) {

          let html = `
          <div class="card" data-module="card" data-number="${this.content[i].id}">
            <div class="card__body">
              <div class="card__info">
                <div class="card__text">${this.content[i].headerText}</div>
                <div class="card__name">${this.content[i].name}</div>
                <div class="card__component">${this.content[i].component}</div>
                <div class="card__text2">  
          `;

          for (let b = 0; b < this.content[i].list.length; b++) {
            html += `<div>${this.content[i].list[b]}</div>`;
          }

          html += `
          </div>
              </div>

              <div class="card__oval">
                <div class="card__weight">${this.content[i].weight}</div>
                <div class="card__unit">${this.content[i].unit}</div>
              </div>

              <div class="card__cat">
                <img src="/img/${this.imgCat}" alt="cat">
              </div>
            </div>
            <div class="card__footer">
              ${this.cardFooter.default}
            </div>

          </div>
          `;

          let cards = document.querySelector('.cards');
          cards.insertAdjacentHTML('beforeend', html);
        }
      }
    },
    clickHandler(e) {

      console.log(e.target.module);

      let div = e.target.closest('.card');

      // console.log(div.dataset.module);

      if (div.dataset.module != 'card') {
        return
      }

      div.classList.toggle('card__selected');

      let numberCard = div.dataset.number;

      if (div.classList.contains('card__selected')) {
        div.querySelector('.card__footer').innerHTML = this.content[numberCard].cardFooter;
      } else {
        div.querySelector('.card__footer').innerHTML = this.cardFooter.default;
      }
      

    },
    listener() {
      let cards = document.querySelector('.cards');
      cards.addEventListener('click', (e) => this.clickHandler(e));
    }
  },
  mounted() {
    this.init('.project');
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
