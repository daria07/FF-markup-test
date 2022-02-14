<template>
    <header> 
      <div class="container">
        <div class="row"> 
          <a class="logo" href="/"> 
            <img src="../assets/img/logo.svg" alt="">
          </a>
          <div class="header-section">
            <a class="menu-btn" href="faq.html">Анкета</a>
            <a class="menu-link" href="faq.html">Выход</a>
          </div>
          <a class="header-cart" href="authorization.html">
            <img src="../assets/img/cart.svg" alt="">
            <span>3</span>
            <span>Cart</span>
          </a>
          <div class="menu-mobile"> 
            <div class="hb-line hb-line-1"></div>
            <div class="hb-line hb-line-2"></div>
            <div class="hb-line hb-line-3"></div>
          </div>
        </div>
      </div>
    </header>
</template>

<style lang="scss">

  header {
    font-size: 14px;
    height: 80px;
    border-bottom: 1px solid #E5E5E5; 

    .row {
      -webkit-box-align: center;
      -ms-flex-align: center;
      align-items: center; 
    }
  }
  
  .logo {
    max-width: 186px;
    margin-right: auto;
    width: 100%; 
  }
  
  .header-section {
    border-left: 1px solid #E5E5E5;
    border-right: 1px solid #E5E5E5;
    padding: 20px 44px 20px 20px; 

    a {
      font-size: 14px;
      line-height: 20px;
    }
  }
  
  .menu-link {
    color: #72BF44; 
  }
  
  .menu-btn {
    padding: 10px 24px;
    margin-right: 45px;
    background: #72BF44;
    border-radius: 3px;
    color: #ffffff;
    display: inline-block; 
  }
  
  .header-cart {
    font-size: 16px;
    line-height: 24px;
    position: relative;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    color: #000000;
    margin-left: 20px; 

    img {
      width: 20px;
      margin-right: 10px; 
    }

    span {
      background: #CC0E00;
      border-radius: 20px;
      font-size: 8px;
      line-height: 14px;
      color: #ffffff;
      display: inline-block;
      width: 14px;
      height: 14px;
      position: absolute;
      top: -7px;
      left: 13px;
      text-align: center; 
    }
  }

  .menu-mobile {
      position: relative;
      display: none;
      width: 20px;
      height: 18px;
    }

  .hb-line {
    height: 2px;
    width: 20px;
    background: #000000;
    position: absolute;
    left: 0;
  }

  .hb-line-1 {
    top: 0;
  }
  .hb-line-2 {
    top: 8px;
    width: 16px;
  }
  .hb-line-3 {
    top: 16px;
  }
  
  @media(max-width: 640px) {
    header {
      height: 66px;
      padding: 20px 5px;
    }

    .logo {
      max-width: 140px;
    }

    .header-cart {
      margin-left: 0;
      margin-right: 25px;

      span:last-child {
        display: none;
      }
    }
    
    .header-section {
      display: none;
    }

    .menu-mobile {
      display: block;
    }

  }

</style>