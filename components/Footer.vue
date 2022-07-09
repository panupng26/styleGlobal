<template>
  <!-- Footer -->
  <footer class="font-small" style="background-color: #001819;">
    <!-- Footer Links -->
    <div class="container text-start text-md-left">
      <div class="d-flex justify-content-between">
        <div class="col-10">
          <div class="row mt-4">
            <!-- Grid column -->
            <div class="col">
              <h6 class="text-white" style="margin-bottom: 0.35em;">
                <strong>MOVEST</strong>
              </h6>
              <p class="pt-2">
                <a :href="`${domain.main}`">
                  หน้าหลัก
                </a>
              </p>
              <p>
                <a :href="`${domain.main}/about`">
                  เกี่ยวกับเรา
                </a>
              </p>
              <p>
                <a :href="`${domain.main}/agent-register}`">
                  สมัครงาน
                </a>
              </p>
            </div>
            <!-- Grid column -->

            <!-- Grid column -->
            <div class="col">
              <h6 class="font-weight-bold text-white">
                ประเภท
              </h6>
              <p class="pt-2">
                <a :href="`${domain.living}`">
                  ซื้อ
                </a>
              </p>
              <p>
                <a :href="`${domain.living}`">
                  ขาย
                </a>
              </p>
              <p>
                <a :href="`${domain.living}`">
                  เช่า
                </a>
              </p>
            </div>
            <!-- Grid column -->

            <!-- Grid column -->
            <div class="col">
              <h6 class="font-weight-bold text-white">
                <!-- <a href="https://dev.living.movest.co/"> -->
                อสังหาฯ
                <!-- </a> -->
              </h6>
              <p class="pt-2">
                <a :href="`${domain.living}/estate`">
                  ค้นหาอสังหา
                </a>
              </p>
              <p>
                <a :href="`${domain.living}`">
                  ฝากทรัพย์
                </a>
              </p>
            </div>
            <!-- Grid column -->

            <!-- Grid column -->
            <div class="col">
              <h6 class="font-weight-bold text-white">
                ตัวแทน
              </h6>
              <p class="pt-2">
                <a :href="`${domain.living}/agent`">
                  ค้นหาตัวแทน
                </a>
              </p>
              <p>
                <a :href="`${domain.living}/agent-register}`">
                  สมัครตัวแทน
                </a>
              </p>
            </div>
            <!-- Grid column -->

            <!-- Grid column -->
            <div class="col">
              <h6 class="font-weight-bold text-white">
                คอร์ส
              </h6>
              <p class="pt-2">
                <a :href="`${domain.learning}/course`">
                  ค้นหาคอร์ส
                </a>
              </p>
              <p>
                <a :href="`${domain.learning}/course`">
                  สอนกับเรา
                </a>
              </p>
            </div>
            <!-- Grid column -->

            <!-- Grid column -->
            <div class="col">
              <!-- Links -->
              <h6 class="font-weight-bold text-white">
                งาน
              </h6>
              <p class="pt-2">
                <a :href="`${domain.jobs}/jobs`">
                  ค้นหางาน
                </a>
              </p>
              <p>
                <a :href="`${domain.jobs}`">
                  รับสมัครงาน
                </a>
              </p>
            </div>
            <!-- Grid column -->

            <!-- Grid column -->
            <div class="col-3">
              <h6 class="font-weight-bold text-white">
                <a :href="`${domain.shopping}/products`">
                  สินค้าและบริการ
                </a>
              </h6>
              <p class="pt-2">
                <a :href="`${domain.shopping}/products`">
                  สินค้า
                </a>
              </p>
              <p>
                <a :href="`${domain.shopping}/products`">
                  บริการ
                </a>
              </p>
              <p>
                <a :href="`${domain.shopping}/products`">
                  เปิดร้านกับเรา
                </a>
              </p>
            </div>
            <!-- Grid column -->
          </div>
        </div>
        <div class="col-2">
          <div class="row text-end mt-4">
            <div class="row">
              <h6 class="font-weight-bold text-white">
                สมาชิก
              </h6>
              <p class="pt-2">
                <a :href="`${domain.main}/register}`">
                  ลงทะเบียน
                </a>
              </p>
              <p>
                <a :href="`${domain.main}/login}`">
                  เข้าสู่ระบบ
                </a>
              </p>
            </div>
            <!-- Grid column -->
          </div>
        </div>
      </div>
      <div class="container">
        <hr style="color: whitesmoke;">
        <div class="d-flex justify-content-between bg-back text-white">
          <div class="d-flex align-items-center">
            <div style="lign-self: center;">
              <span>
                <!-- {{ $t('footer') }} -->
                © 2021 movest.co
              </span>
            </div>
            <div class="pl-5 px-3">
              <span>
                Terms
              </span>
            </div>
            <div class="">
              <span>
                Privacy Policy
              </span>
            </div>
          </div>
          <!-- <div class="col-2 d-flex align-items-center layout-p">
            <p class="layout-p">
              PDPA
            </p>
          </div> -->
          <div>
            <div style="text-align: end;">
              <a href="https://www.facebook.com/Recruith">
                <a-button shape="circle" style="width: 1.5rem; height: 2rem; margin-right: 0.5em; color: rgb(46, 48, 50)">
                  <svg-icon icon-name="facebook" style="font-size:1.5em;" />
                </a-button>
              </a>
              <a href="https://www.linkedin.com/company/53202061">
                <a-button shape="circle" style="width: 1.5rem; height: 2rem; margin: 0.5em; color: rgb(46, 48, 50)">
                  <!-- <svg-icon icon-name="linkin" style="font-size:1.5em;" /> -->
                  <a-icon type="linkedin" style="font-size:1.5em !important;" />
                </a-button>
              </a>
              <a href="">
                <a-button shape="circle" style="width: 1.5rem; height: 2rem; margin: 0.5em; color: rgb(46, 48, 50)">
                  <svg-icon icon-name="line" style="font-size:1.5em !important;" />
                </a-button>
              </a>
              <a :href="`mailto:contact@movest.co`">
                <a-button shape="circle" style="width: 1.5rem; height: 2rem; margin: 0.5em; color: rgb(46, 48, 50);">
                  <svg-icon icon-name="mail" style="font-size:1.5em;" />
                </a-button>
              </a>
              <a :href="`tel:086-881-4819`">
                <a-button shape="circle" style="width: 1.5rem; height: 2rem; margin: 0.5em; color: rgb(46, 48, 50);">
                  <svg-icon icon-name="call" style="font-size:1.5em;" />
                </a-button>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Footer Links -->

    <!-- Copyright -->

  <!-- Copyright -->
  </footer>
<!-- Footer -->
</template>
<script>
export default {
  data () {
    return {
      domain: {
        main: null,
        living: null,
        learning: null,
        shopping: null,
        jobs: null,
        checkout: null
      }
    }
  },
  mounted () {
    this.domain = {
      main: process.env.REDIRECT_MAIN,
      living: process.env.REDIRECT_LIVING,
      learning: process.env.REDIRECT_LEARNING,
      shopping: process.env.REDIRECT_SHOPPING,
      jobs: process.env.REDIRECT_JOBS,
      checkout: process.env.REDIRECT_CHECKOUT
    }
  }
}
</script>
<style scoped>
.text-white{
  color: whitesmoke;
}
p{
  margin-bottom: 0.5em;
}
.layout-p{
  margin-bottom: 0em;
  padding: 0px;
}
.h1{
  margin-bottom: 0 rem;
}
.font-weight-bold{
  font-weight: 400 !important;
  font-size: 18px;
}
a{
  font-weight: 300;
  color: whitesmoke;
}
</style>
