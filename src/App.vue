<script setup>
import { ref } from 'vue';
import html2canvas from 'html2canvas';
import jsPDF from 'jspdf';

const print = (id = 'section') => {
  html2canvas(document.getElementById(id), {
    allowTaint: true,//允许跨域
    height: document.getElementById(id).scrollHeight,//
    width: document.getElementById(id).scrollWidth,//为了使横向滚动条的内容全部展示，这里必须指定
    useCORS: true, //解决图片跨域问题
  }).then(canvas => {
    const contentWidth = canvas.width;
    const contentHeight = canvas.height;

    //一页pdf显示html页面生成的canvas高度;
    const pageHeight = contentWidth / 592.28 * 841.89;
    //未生成pdf的html页面高度
    let leftHeight = contentHeight;
    //页面偏移
    let position = 0;
    //a4纸的尺寸\[595.28,841.89\]，html页面生成的canvas在pdf中图片的宽高
    const imgWidth = 595.28;
    const imgHeight = 592.28 / contentWidth * contentHeight;

    const pageData = canvas.toDataURL('image/jpeg', 1.0);

    const pdf = new jsPDF('', 'pt', 'a4');

    //有两个高度需要区分，一个是html页面的实际高度，和生成pdf的页面高度(841.89)
    //当内容未超过pdf一页显示的范围，无需分页
    if (leftHeight < pageHeight) {
      pdf.addImage(pageData, 'JPEG', 0, 0, imgWidth, imgHeight );
    } else {
      while(leftHeight > 0) {
        pdf.addImage(pageData, 'JPEG', 0, position, imgWidth, imgHeight)
        leftHeight -= pageHeight;
        position -= 841.89;
        //避免添加空白页
        if(leftHeight > 0) {
          pdf.addPage();
        }
      }
    }

    pdf.save('content.pdf');
  });
}
</script>

<template>
  <div>
    <button class="btn btn-outline btn-primary ml-auto flex" @click="print('section')">打印</button>
  </div>


  <!-- Section Testimonial -->
  <div id="section">
    <section id="section1">
      <!-- Container -->
      <div class="mx-auto w-full max-w-5xl px-5 py-16 md:px-10 md:py-24 lg:py-32">
        <!-- Title -->
        <h2 class="mb-8 text-center text-3xl font-bold md:mb-14 md:text-5xl"> What our clients are saying </h2>
        <!-- Testimonial List-->
        <ul class="grid gap-8 sm:grid-cols-2">
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cb5e3ea08ab4c244194a_Ellipse%205-4.png" alt="" class="mr-4 h-16 w-16" />
              <div class="f">
                <h6 class="font-bold">Laila Bahar</h6>
                <p class="text-sm text-[#636262]">Designer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cb67bf1bca198e298c35_Ellipse%205-2.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Amy Crouch</h6>
                <p class="text-sm text-[#636262]">Webflow Designer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cb614a296368b383467c_Ellipse%205-3.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Kim Menor</h6>
                <p class="text-sm text-[#636262]">Webflow Developer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cfcd4e55dd261e3fce8b_Ellipse%205-5.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Nathan Smich</h6>
                <p class="text-sm text-[#636262]">Product Manager</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cfd73c2bb8cd5b2c4662_Ellipse%205-6.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Martin Midtbo</h6>
                <p class="text-sm text-[#636262]">Designer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cfd05b21e9eda63baa9b_Ellipse%205-7.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Amy Lackler</h6>
                <p class="text-sm text-[#636262]">Designer</p>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </section>
    <section id="section2">
      <!-- Container -->
      <div class="mx-auto w-full max-w-5xl px-5 py-16 md:px-10 md:py-24 lg:py-32">
        <!-- Title -->
        <h2 class="mb-8 text-center text-3xl font-bold md:mb-14 md:text-5xl"> What our clients are saying </h2>
        <!-- Testimonial List-->
        <ul class="grid gap-8 sm:grid-cols-2">
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cb5e3ea08ab4c244194a_Ellipse%205-4.png" alt="" class="mr-4 h-16 w-16" />
              <div class="f">
                <h6 class="font-bold">Laila Bahar</h6>
                <p class="text-sm text-[#636262]">Designer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cb67bf1bca198e298c35_Ellipse%205-2.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Amy Crouch</h6>
                <p class="text-sm text-[#636262]">Webflow Designer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cb614a296368b383467c_Ellipse%205-3.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Kim Menor</h6>
                <p class="text-sm text-[#636262]">Webflow Developer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cfcd4e55dd261e3fce8b_Ellipse%205-5.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Nathan Smich</h6>
                <p class="text-sm text-[#636262]">Product Manager</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cfd73c2bb8cd5b2c4662_Ellipse%205-6.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Martin Midtbo</h6>
                <p class="text-sm text-[#636262]">Designer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cfd05b21e9eda63baa9b_Ellipse%205-7.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Amy Lackler</h6>
                <p class="text-sm text-[#636262]">Designer</p>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </section>
    <section id="section3">
      <!-- Container -->
      <div class="mx-auto w-full max-w-5xl px-5 py-16 md:px-10 md:py-24 lg:py-32">
        <!-- Title -->
        <h2 class="mb-8 text-center text-3xl font-bold md:mb-14 md:text-5xl"> What our clients are saying </h2>
        <!-- Testimonial List-->
        <ul class="grid gap-8 sm:grid-cols-2">
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cb5e3ea08ab4c244194a_Ellipse%205-4.png" alt="" class="mr-4 h-16 w-16" />
              <div class="f">
                <h6 class="font-bold">Laila Bahar</h6>
                <p class="text-sm text-[#636262]">Designer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cb67bf1bca198e298c35_Ellipse%205-2.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Amy Crouch</h6>
                <p class="text-sm text-[#636262]">Webflow Designer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cb614a296368b383467c_Ellipse%205-3.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Kim Menor</h6>
                <p class="text-sm text-[#636262]">Webflow Developer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cfcd4e55dd261e3fce8b_Ellipse%205-5.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Nathan Smich</h6>
                <p class="text-sm text-[#636262]">Product Manager</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cfd73c2bb8cd5b2c4662_Ellipse%205-6.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Martin Midtbo</h6>
                <p class="text-sm text-[#636262]">Designer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cfd05b21e9eda63baa9b_Ellipse%205-7.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Amy Lackler</h6>
                <p class="text-sm text-[#636262]">Designer</p>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </section>
    <section id="section4">
      <!-- Container -->
      <div class="mx-auto w-full max-w-5xl px-5 py-16 md:px-10 md:py-24 lg:py-32">
        <!-- Title -->
        <h2 class="mb-8 text-center text-3xl font-bold md:mb-14 md:text-5xl"> What our clients are saying </h2>
        <!-- Testimonial List-->
        <ul class="grid gap-8 sm:grid-cols-2">
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cb5e3ea08ab4c244194a_Ellipse%205-4.png" alt="" class="mr-4 h-16 w-16" />
              <div class="f">
                <h6 class="font-bold">Laila Bahar</h6>
                <p class="text-sm text-[#636262]">Designer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cb67bf1bca198e298c35_Ellipse%205-2.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Amy Crouch</h6>
                <p class="text-sm text-[#636262]">Webflow Designer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cb614a296368b383467c_Ellipse%205-3.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Kim Menor</h6>
                <p class="text-sm text-[#636262]">Webflow Developer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cfcd4e55dd261e3fce8b_Ellipse%205-5.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Nathan Smich</h6>
                <p class="text-sm text-[#636262]">Product Manager</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cfd73c2bb8cd5b2c4662_Ellipse%205-6.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Martin Midtbo</h6>
                <p class="text-sm text-[#636262]">Designer</p>
              </div>
            </div>
          </li>
          <li>
            <div class="mb-5 max-w-sm rounded-br-[99px] rounded-tl-[60px] rounded-tr-[99px] bg-[#f2f2f7] px-8 py-6 md:mb-8">
              <p class="text-[#647084]"> “Lorem ipsum dolor sit amet, &nbsp;elit ut aliquam, purus sit amet luctus venenatis elit ut aliquam, purus sit amet luctus venenatis" </p>
            </div>
            <div class="mb-5 flex lg:mb-8">
              <img src="https://assets.website-files.com/6357722e2a5f19121d37f84d/6358cfd05b21e9eda63baa9b_Ellipse%205-7.png" alt="" class="mr-4 h-16 w-16" />
              <div class="flex flex-col">
                <h6 class="font-bold">Amy Lackler</h6>
                <p class="text-sm text-[#636262]">Designer</p>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </section>
  </div>
</template>

<style scoped>
iframe {
  width: 1px;
  min-width: 100%;
}
</style>
