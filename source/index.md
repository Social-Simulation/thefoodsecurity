---
title: Home
comments: false
toc: false
layout: homepage
---
<div class="activity-gallery">
    <div class="swiper-container">
        <div class="swiper-wrapper">
            <div class="swiper-slide init">
                <div class="inner">
                    <a href="/events/2024">
                        <figure><img src="./2024.jpg"></figure>
                    </a>
                </div>
            </div>
            <div class="swiper-slide init">
                <div class="inner">
                    <a href="/about/">
                        <figure><img src="https://wp-img.daozhao.com/thefoodsecurity/Carousel_food1710.png"></figure>
                    </a>
                </div>
            </div>
            <div class="swiper-slide init">
                <div class="inner">
                    <a href="/initiative/">
                        <figure><img src="https://wp-img.daozhao.com/thefoodsecurity/Carousel_rice1995.png"></figure>
                    </a>
                </div>
            </div>
        </div>
        <div class="swiper-button-prev"></div>
        <!--左箭头-->
        <div class="swiper-button-next"></div>
        <!--右箭头-->
    </div>
</div>

<script>
    var swiper = new Swiper('.swiper-container', {
        speed: 700,
        slidesPerView: 'auto',
        centeredSlides: true,
        autoplay:true,
        loop: true,
        on: {
            init: function() {
                this.slides.removeClass('init');
            },
        },
        navigation: {
            nextEl: '.swiper-button-next',
            prevEl: '.swiper-button-prev',
        },
    });
    swiper.$el.parent('.activity-gallery')[0].onmouseover = function() {
        swiper.$el.addClass('mouse-hover');
    };
    swiper.$el.parent('.activity-gallery')[0].onmouseout = function() {
        swiper.$el.removeClass('mouse-hover');
    };
</script>
