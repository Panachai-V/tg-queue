<template>
  <Topnav :user="user" />
  <Sidenav :user="user" :activeIndex="sidenavActiveIndex" />

  <section class="section-full pull-right">
    <div class="container">
      <form action="/admin/companies" method="GET" @submit="onSubmit">

        <div class="section-header mb-4" data-aos="fade-up" data-aos-delay="0">
          <div class="btns mt-0">
            <a href="/admin/companies" class="btn color-gray h-color-01">
              <img class="icon-prepend xs" src="/assets/img/icon/chev-left.svg" alt="Image Icon" />
              ย้อนกลับ
            </a>
          </div>
          <div class="header-wrapper">
            <div class="text-container">
              <h6 class="h3">Edit Company</h6>
            </div>
            <div class="btns hide-mobile">
              <Button 
                text="ลบ" href="javascript:" @click="openedPopupDelete = !openedPopupDelete" 
                classer="btn-color-06 mr-2" :prepend="true" icon="close-white.svg" 
              />
              <Button 
                type="submit" text="แก้ไข" 
                classer="btn-color-01" :prepend="true" icon="check-white.svg" 
              />
            </div>
            <div class="btns show-mobile">
              <Button 
                text="ลบ" href="javascript:" @click="openedPopupDelete = !openedPopupDelete" 
                classer="btn-color-06 btn-sm mr-1" 
              />
              <Button type="submit" text="แก้ไข" classer="btn-color-01 btn-sm" />
            </div>
          </div>
        </div>

        <div class="stripe section-px border-bottom bcolor-fgray" data-aos="fade-up" data-aos-delay="150">
          <p class="fw-400">ข้อมูลทั่วไป</p>
        </div>
        <div class="section-px section-py-grid" data-aos="fade-up" data-aos-delay="150">
          <div class="grids">
            <div class="grid xl-10 lg-15 md-20 sm-30 xs-50">
              <FormGroup 
                type="select" label="คำนำหน้า *" 
                :value="dataset.prefix" @input="dataset.prefix = $event" 
                :options="[
                  { value: 'นาย', text: 'นาย' },
                  { value: 'นาง', text: 'นาง' },
                  { value: 'นางสาว', text: 'นางสาว' }
                ]"
              />
            </div>
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="text" label="ชื่อ *" placeholder="โปรดระบุ" 
                :value="dataset.firstname" @input="dataset.firstname = $event" 
                :errorText="isValidated && !dataset.firstname? 'กรุณาระบุ': ''" 
                :classer="isValidated && !dataset.firstname? 'error': ''" 
              />
            </div>
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="text" label="นามสกุล *" placeholder="โปรดระบุ" 
                :value="dataset.lastname" @input="dataset.lastname = $event" 
                :errorText="isValidated && !dataset.lastname? 'กรุณาระบุ': ''" 
                :classer="isValidated && !dataset.lastname? 'error': ''" 
              />
            </div>
            <div class="sep"></div>
            
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="text" label="เบอร์โทรศัพท์" placeholder="โปรดระบุ" 
                :value="dataset.phone" @input="dataset.phone = $event" 
              />
            </div>
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="file-image" label="รูปโปรไฟล์" 
              />
            </div>
            <div class="sep"></div>
            
            <div class="grid lg-60 md-80 sm-100">
              <FormGroup 
                type="textarea" label="ที่อยู่ *" placeholder="โปรดระบุ" 
                :value="dataset.address" @input="dataset.address = $event" 
                :errorText="isValidated && !dataset.address? 'กรุณาระบุ': ''" 
                :classer="isValidated && !dataset.address? 'error': ''" 
              />
            </div>
            <div class="sep"></div>
            
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="text" label="จังหวัด *" placeholder="โปรดระบุ" 
                :value="dataset.province" @input="dataset.province = $event" 
                :errorText="isValidated && !dataset.province? 'กรุณาระบุ': ''" 
                :classer="isValidated && !dataset.province? 'error': ''" 
              />
            </div>
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="text" label="รหัสไปรษณีย์ *" placeholder="โปรดระบุ" 
                :value="dataset.zipcode" @input="dataset.zipcode = $event" 
                :errorText="isValidated && !dataset.zipcode? 'กรุณาระบุ': ''" 
                :classer="isValidated && !dataset.zipcode? 'error': ''" 
              />
            </div>
          </div>
        </div>
        
        <div class="stripe section-px border-bottom bcolor-fgray" data-aos="fade-up" data-aos-delay="150">
          <p class="fw-400">ข้อมูลบริษัท</p>
        </div>
        <div class="section-px section-py-grid" data-aos="fade-up" data-aos-delay="150">
          <div class="grids">
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="text" label="ชื่อบริษัท *" placeholder="โปรดระบุ" 
                :value="dataset.company" @input="dataset.company = $event" 
                :errorText="isValidated && !dataset.company? 'กรุณาระบุ': ''" 
                :classer="isValidated && !dataset.company? 'error': ''" 
              />
            </div>
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="text" label="เบอร์โทรบริษัท" placeholder="โปรดระบุ" 
                :value="dataset.companyPhone" @input="dataset.companyPhone = $event" 
              />
            </div>
            <div class="sep"></div>
            
            <div class="grid lg-60 md-80 sm-100">
              <FormGroup 
                type="textarea" label="ที่อยู่บริษัท *" placeholder="โปรดระบุ" 
                :value="dataset.companyAddress" @input="dataset.companyAddress = $event" 
                :errorText="isValidated && !dataset.companyAddress? 'กรุณาระบุ': ''" 
                :classer="isValidated && !dataset.companyAddress? 'error': ''" 
              />
            </div>
            <div class="sep"></div>
            
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="text" label="จังหวัด *" placeholder="โปรดระบุ" 
                :value="dataset.companyProvince" @input="dataset.companyProvince = $event" 
                :errorText="isValidated && !dataset.companyProvince? 'กรุณาระบุ': ''" 
                :classer="isValidated && !dataset.companyProvince? 'error': ''" 
              />
            </div>
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="text" label="รหัสไปรษณีย์ *" placeholder="โปรดระบุ" 
                :value="dataset.companyZipcode" @input="dataset.companyZipcode = $event" 
                :errorText="isValidated && !dataset.companyZipcode? 'กรุณาระบุ': ''" 
                :classer="isValidated && !dataset.companyZipcode? 'error': ''" 
              />
            </div>
          </div>
        </div>
        
        <div class="stripe section-px border-bottom bcolor-fgray" data-aos="fade-up" data-aos-delay="150">
          <p class="fw-400">บัญชีผู้ใช้</p>
        </div>
        <div class="section-px section-py-grid" data-aos="fade-up" data-aos-delay="150">
          <div class="grids">
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="text" label="ชื่อผู้ใช้ *" placeholder="โปรดระบุ" 
                :value="dataset.username" @input="dataset.username = $event" 
                :errorText="isValidated && !dataset.username? 'กรุณาระบุ': ''" 
                :classer="isValidated && !dataset.username? 'error': ''" 
              />
            </div>
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="email" label="อีเมล *" placeholder="โปรดระบุ" 
                :value="dataset.email" @input="dataset.email = $event" 
                :errorText="isValidated && !dataset.email? 'กรุณาระบุ': ''" 
                :classer="isValidated && !dataset.email? 'error': ''" 
              />
            </div>
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="select" label="สถานะ" placeholder="โปรดเลือก" 
                :value="dataset.status" @input="dataset.status = $event" 
                :options="[
                  { value: 1, text: 'เปิดใช้งาน' },
                  { value: 0, text: 'ปิดใช้งาน' }
                ]"
              />
            </div>
            <div class="sep"></div>
            
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="password" label="รหัสผ่าน *" placeholder="โปรดระบุ" 
                :value="dataset.password" @input="dataset.password = $event" 
                :errorText="isValidated && !dataset.password? 'กรุณาระบุ': ''" 
                :classer="isValidated && !dataset.password? 'error': ''" 
              />
            </div>
            <div class="grid lg-30 md-40 sm-100">
              <FormGroup 
                type="password" label="ยืนยันรหัสผ่าน *" placeholder="โปรดระบุ" 
                :value="dataset.confPassword" @input="dataset.confPassword = $event" 
                :errorText="isValidated && !dataset.confPassword? 'กรุณาระบุ': ''" 
                :classer="isValidated && !dataset.confPassword? 'error': ''" 
              />
            </div>
          </div>
        </div>

      </form>
      
      <div class="stripe section-px border-bottom bcolor-fgray" data-aos="fade-up" data-aos-delay="150">
        <p class="fw-400">พนักงานขับรถ</p>
      </div>
      <div class="pb-2" data-aos="fade-up" data-aos-delay="150">
        <DataTable 
          :rows="rows1" 
          :columns="[
            { key: 'avatar', text: 'รูปโปรไฟล์' },
            { key: 'username', text: 'บัญชีผู้ใช้' },
            { key: 'firstname', text: 'ชื่อจริง' },
            { key: 'lastname', text: 'นามสกุล' },
            { key: 'email', text: 'อีเมล' },
            { key: 'status', text: 'สถานะ' },
            { key: 'options', classer: 'options' }
          ]" 
          :search="[ 'username', 'firstname', 'lastname', 'email' ]" 
          :orders="[
            { key: 'username-asc', text: 'ชื่อบัญชีผู้ใช้ (ใหม่สุด)' },
            { key: 'username-desc', text: 'ชื่อบัญชีผู้ใช้ (เก่าสุด)' },
            { key: 'firstname-desc', text: 'ชื่อจริง (ใหม่สุด)' },
            { key: 'firstname-asc', text: 'ชื่อจริง (เก่าสุด)' },
            { key: 'lastname-desc', text: 'นามสกุล (ใหม่สุด)' },
            { key: 'lastname-asc', text: 'นามสกุล (เก่าสุด)' },
            { key: 'email-desc', text: 'อีเมล (ใหม่สุด)' },
            { key: 'email-asc', text: 'อีเมล (เก่าสุด)' }
          ]" 
          :groups="{
            filter: 'status',
            options: [
              { text: 'เปิดใช้งาน', value: 1, checked: true },
              { text: 'ปิดใช้งาน', value: 0, checked: true }
            ]
          }" 
          @click-view="(id)=>openDriverView(id)" 
          @click-edit="(id)=>openDriverEdit(id)" 
        />
      </div>
    </div>
  </section>
  
  <!-- Popup Delete -->
  <div class="popup-container" :class="{ 'active': openedPopupDelete }">
    <div class="wrapper">
      <div class="close-filter" @click="openedPopupDelete = !openedPopupDelete"></div>
      <form action="/admin/companies" method="GET" class="w-full">
        <div class="popup-box">
          <div class="header">
            <div class="btns mt-0">
              <a href="javascript:" class="btn btn-close" @click="openedPopupDelete = !openedPopupDelete">
                <img class="icon-prepend xs" src="/assets/img/icon/close.svg" alt="Image Icon" />
                ปิดหน้าต่าง
              </a>
            </div>
            <div class="header-wrapper">
              <div class="text-container">
                <h6 class="h3">ยืนยันการลบ</h6>
              </div>
              <div class="btns hide-mobile">
                <Button 
                  type="submit" text="ลบ" classer="btn-color-06 mr-2" 
                  :prepend="true" icon="close-white.svg" 
                />
                <Button 
                  text="ปิด" href="javascript:" classer="btn-color-08" 
                  @click="openedPopupDelete = !openedPopupDelete"
                />
              </div>
              <div class="btns show-mobile">
                <Button 
                  type="submit" text="ลบ" classer="btn-color-06 btn-sm mr-1" 
                />
                <Button 
                  text="ปิด" href="javascript:" classer="btn-color-08 btn-sm" 
                  @click="openedPopupDelete = !openedPopupDelete"
                />
              </div>
            </div>
          </div>
          <div class="body pt-4 pb-5">
            <p class="color-gray">หมายเหตุ</p>
            <p class="mt-2">
              หมายเลขประจำตัวผู้ป่วยที่คุณค้นหาอาจจะ ไม่ถูกต้อง คุณสามารถ “ปิดหน้าต่าง” 
              เพื่อระบุหมายเลขประจำตัวผู้ป่วยใหม่อีกครั้ง หรือ ผู้ป่วยที่คุณต้องการหา อาจจะ ไม่มีข้อมูลในระบบ 
              คุณสามารถเพิ่มข้อมูลผู้ป่วยใหม่ โดยการคลิกที่ปุ่ม “เพิ่มข้อมูล”
            </p>
          </div>
        </div>
      </form>
    </div>
  </div>
  
  <!-- Driver View -->
  <div class="popup-container" :class="{ 'active': openedDriverView }">
    <div class="wrapper">
      <div class="close-filter" @click="openedDriverView = !openedDriverView"></div>
      <div class="popup-box md">
        <div class="header">
          <div class="btns mt-0">
            <a href="javascript:" class="btn btn-close" @click="openedDriverView = !openedDriverView">
              <img class="icon-prepend xs" src="/assets/img/icon/close.svg" alt="Image Icon" />
              ปิดหน้าต่าง
            </a>
          </div>
          <div class="header-wrapper">
            <div class="text-container">
              <h6 class="h3">View Driver</h6>
            </div>
            <div class="btns hide-mobile">
              <Button 
                text="ปิด" href="javascript:" classer="btn-color-08" 
                @click="openedDriverView = !openedDriverView"
              />
            </div>
            <div class="btns show-mobile">
              <Button 
                text="ปิด" href="javascript:" classer="btn-color-08 btn-sm" 
                @click="openedDriverView = !openedDriverView"
              />
            </div>
          </div>
        </div>
        <div class="body-wrapper">
          <div class="stripe border-bottom bcolor-fgray pl-0 pr-0">
            <div class="body pt-0 pb-0">
              <p class="fw-400">ข้อมูลทั่วไป</p>
            </div>
          </div>
          <div class="body pb-5">
            <div class="grids">
              <div class="grid sm-25">
                <FormGroup type="plain" label="คำนำหน้า" value="นาย" />
              </div>
              <div class="grid sm-1-3 xs-50">
                <FormGroup type="plain" label="ชื่อ" value="จริงใจ" />
              </div>
              <div class="grid sm-1-3 xs-50">
                <FormGroup type="plain" label="นามสกุล" value="ใจมั่นคง" />
              </div>
              <div class="sep"></div>
          
              <div class="grid sm-50 xs-50">
                <FormGroup type="plain" label="เบอร์โทรศัพท์" value="091-234 5678" />
              </div>
              <div class="grid sm-50 xs-50">
                <FormGroup type="plain" label="รูปโปรไฟล์" />
              </div>
              <div class="sep"></div>
          
              <div class="grid sm-100">
                <FormGroup type="plain" label="ที่อยู่" value="Racha Thewa, Bang Phli District" />
              </div>
              <div class="sep"></div>
              
              <div class="grid sm-50 xs-50">
                <FormGroup type="plain" label="จังหวัด" value="Samut Prakan" />
              </div>
              <div class="grid sm-50 xs-50">
                <FormGroup type="plain" label="รหัสไปรษณีย์" value="10540" />
              </div>
            </div>
          </div>
          
          <div class="stripe border-bottom bcolor-fgray pl-0 pr-0">
            <div class="body pt-0 pb-0">
              <p class="fw-400">บัญชีผู้ใช้</p>
            </div>
          </div>
          <div class="body pb-5">
            <div class="grids">
              <div class="grid md-1-3 sm-50 xs-50">
                <FormGroup type="plain" label="ชื่อผู้ใช้" value="User0001" />
              </div>
              <div class="grid md-1-3 sm-50 xs-50">
                <FormGroup type="plain" label="อีเมล" value="employee@gmail.com" />
              </div>
              <div class="grid md-1-3 sm-50 xs-50">
                <FormGroup type="plain" label="สถานะ" value="เปิดใช้งาน" />
              </div>
            </div>
          </div>

          <div class="stripe border-bottom bcolor-fgray pl-0 pr-0">
            <div class="body pt-0 pb-0">
              <p class="fw-400">ภาพรวม</p>
            </div>
          </div>
          <div class="body">
            <div class="grids">
              <div class="grid sm-50">
                <SpecialCard03 
                  label="งานที่สำเร็จแล้ว" :count="48" unit="งาน" 
                  classer="sm no-hover"
                />
              </div>
              <div class="grid sm-50">
                <SpecialCard03 
                  label="ความพึงพอใจโดยรวม" :count="4.68" unit="/ 5" 
                  classer="sm no-hover"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  
  <!-- Driver Edit -->
  <div class="popup-container" :class="{ 'active': openedDriverEdit }">
    <div class="wrapper">
      <div class="close-filter" @click="openedDriverEdit = !openedDriverEdit"></div>
      <form class="w-full" action="/" method="GET" @submit="onSubmitDriverEdit">
        <div class="popup-box md">
          <div class="header">
            <div class="btns mt-0">
              <a href="javascript:" class="btn btn-close" @click="openedDriverEdit = !openedDriverEdit">
                <img class="icon-prepend xs" src="/assets/img/icon/close.svg" alt="Image Icon" />
                ปิดหน้าต่าง
              </a>
            </div>
            <div class="header-wrapper">
              <div class="text-container">
                <h6 class="h3">Edit Driver</h6>
              </div>
              <div class="btns hide-mobile">
                <Button 
                  type="submit" text="แก้ไข" 
                  classer="btn-color-01 mr-2" :prepend="true" icon="check-white.svg" 
                />
                <Button 
                  text="ปิด" href="javascript:" classer="btn-color-08" 
                  @click="openedDriverEdit = !openedDriverEdit"
                />
              </div>
              <div class="btns show-mobile">
                <Button 
                  type="submit" text="แก้ไข" classer="btn-color-01 btn-sm mr-1"
                />
                <Button 
                  text="ปิด" href="javascript:" classer="btn-color-08 btn-sm" 
                  @click="openedDriverEdit = !openedDriverEdit"
                />
              </div>
            </div>
          </div>
          <div class="body-wrapper">
            <div class="stripe border-bottom bcolor-fgray pl-0 pr-0">
              <div class="body pt-0 pb-0">
                <p class="fw-400">ข้อมูลทั่วไป</p>
              </div>
            </div>
            <div class="body pb-5">
              <div class="grids">
                <div class="grid sm-25">
                  <FormGroup 
                    type="select" label="คำนำหน้า *" 
                    value="นาย" :required="true" 
                    :options="[
                      { value: 'นาย', text: 'นาย' },
                      { value: 'นาง', text: 'นาง' },
                      { value: 'นางสาว', text: 'นางสาว' }
                    ]"
                  />
                </div>
                <div class="grid sm-1-3 xs-50">
                  <FormGroup 
                    type="text" label="ชื่อ *" placeholder="โปรดระบุ" 
                    value="จริงใจ" :required="true" 
                  />
                </div>
                <div class="grid sm-1-3 xs-50">
                  <FormGroup 
                    type="text" label="นามสกุล *" placeholder="โปรดระบุ" 
                    value="ใจมั่นคง" :required="true" 
                  />
                </div>
                <div class="sep"></div>
            
                <div class="grid sm-50 xs-50">
                  <FormGroup 
                    type="text" label="เบอร์โทรศัพท์" placeholder="โปรดระบุ" 
                    value="เบอร์โทรศัพท์" 
                  />
                </div>
                <div class="grid sm-50 xs-50">
                  <FormGroup 
                    type="file-image" label="รูปโปรไฟล์" 
                  />
                </div>
                <div class="sep"></div>
            
                <div class="grid sm-100">
                  <FormGroup 
                    type="textarea" label="ที่อยู่ *" placeholder="โปรดระบุ" 
                    value="Racha Thewa, Bang Phli District" 
                    :required="true" 
                  />
                </div>
                <div class="sep"></div>
                
                <div class="grid sm-50 xs-50">
                  <FormGroup 
                    type="text" label="จังหวัด *" placeholder="โปรดระบุ" 
                    value="Samut Prakan" :required="true" 
                  />
                </div>
                <div class="grid sm-50 xs-50">
                  <FormGroup 
                    type="text" label="รหัสไปรษณีย์ *" placeholder="โปรดระบุ" 
                    value="10540" :required="true" 
                  />
                </div>
              </div>
            </div>
            
            <div class="stripe border-bottom bcolor-fgray pl-0 pr-0">
              <div class="body pt-0 pb-0">
                <p class="fw-400">บัญชีผู้ใช้</p>
              </div>
            </div>
            <div class="body pb-5">
              <div class="grids">
                <div class="grid md-1-3 sm-50 xs-50">
                  <FormGroup 
                    type="text" label="ชื่อผู้ใช้ *" placeholder="โปรดระบุ" 
                    value="User0001" :required="true" 
                  />
                </div>
                <div class="grid md-1-3 sm-50 xs-50">
                  <FormGroup 
                    type="email" label="อีเมล *" placeholder="โปรดระบุ" 
                    value="employee@gmail.com" :required="true" 
                  />
                </div>
                <div class="grid md-1-3 sm-50 xs-50">
                  <FormGroup 
                    type="select" label="สถานะ" placeholder="โปรดเลือก" 
                    :value="1" 
                    :options="[
                      { value: 1, text: 'เปิดใช้งาน' },
                      { value: 0, text: 'ปิดใช้งาน' }
                    ]"
                  />
                </div>
                <div class="sep"></div>
                <div class="grid sm-50">
                  <FormGroup 
                    type="password" label="รหัสผ่าน" placeholder="โปรดระบุ" 
                  />
                </div>
                <div class="grid sm-50">
                  <FormGroup 
                    type="password" label="ยืนยันรหัสผ่าน" placeholder="โปรดระบุ" 
                  />
                </div>
              </div>
            </div>

            <div class="stripe border-bottom bcolor-fgray pl-0 pr-0">
              <div class="body pt-0 pb-0">
                <p class="fw-400">ภาพรวม</p>
              </div>
            </div>
            <div class="body">
              <div class="grids">
                <div class="grid sm-50">
                  <SpecialCard03 
                    label="งานที่สำเร็จแล้ว" :count="48" unit="งาน" 
                    classer="sm no-hover"
                  />
                </div>
                <div class="grid sm-50">
                  <SpecialCard03 
                    label="ความพึงพอใจโดยรวม" :count="4.68" unit="/ 5" 
                    classer="sm no-hover"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Topnav from '../../components/Topnav';
import Sidenav from '../../components/Sidenav';
import DataTable from '../../components/DataTable';
import SpecialCard03 from '../../components/SpecialCard03';

export default {
  name: 'AdminCompanyEditPage',
  components: {
    Topnav,
    Sidenav,
    DataTable,
    SpecialCard03
  },
  data() {
    return {
      sidenavActiveIndex: 3,
      user: {
        id: 1,
        role: 'Admin', /* Product Owner, Company, Driver, Admin */
        company: 'บริษัท พีอาร์เดริเวรี่ จำกัด',
        username: 'General User',
        prefix: 'นาย',
        firstname: 'สมศักดิ์',
        lastname: 'จริงใจ',
        email: 'user@gmail.com',
        phone: '081-1123456',
        avatar: '/assets/img/misc/profile.jpg'
      },

      openedPopupDelete: false,
      isValidated: false,
      dataset: {
        prefix: 'นาย',
        firstname: 'จริงใจ',
        lastname: 'ใจมั่นคง',
        phone: '091-234 5678',
        address: 'Racha Thewa, Bang Phli District',
        province: 'Samut Prakan',
        zipcode: '10540',

        company: 'บริษัท พีอาร์เดริเวรี่ จำกัด',
        companyPhone: '',
        companyAddress: 'Racha Thewa, Bang Phli District',
        companyProvince: 'Samut Prakan',
        companyZipcode: '10540',
        
        username: 'User0001',
        email: 'employee@gmail.com',
        password: '',
        confPassword: '',
        status: 1,
      },

      openedDriverView: false,
      openedDriverEdit: false,
      rows1: []
    }
  },
  created() {
    AOS.init({ easing: 'ease-in-out-cubic', duration: 750, once: true, offset: 10 });
    document.getElementById('color_style').href = '/assets/css/color-admin.css';
    for(var i=0; i<8; i++){
      if(i<2){
        this.rows1.push({
          avatar: { type: 'avatar', text: '/assets/img/misc/profile.jpg' },
          username: { text: 'User000'+i },
          firstname: { text: 'นาย จริงใจ' },
          lastname: { text: 'ใจมั่นคง' },
          email: { text: 'employee@gmail.com' },
          status: { type: 'tag', value: 0, text: 'ปิดใช้งาน', classer: 'ss-tag-danger' },
          options: {
            type: 'options',
            view: { type: 'emit', id: i, href: '/company/driver-view' },
            edit: { type: 'emit', id: i, href: '/company/driver-edit' }
          }
        });
      }else{
        this.rows1.push({
          avatar: { type: 'avatar', text: '/assets/img/misc/profile.jpg' },
          username: { text: 'User000'+i },
          firstname: { text: 'นาย จริงใจ' },
          lastname: { text: 'ใจมั่นคง' },
          email: { text: 'employee@gmail.com' },
          status: { type: 'tag', value: 1, text: 'เปิดใช้งาน', classer: 'ss-tag-success' },
          options: {
            type: 'options',
            view: { type: 'emit', id: i, href: '/company/driver-view' },
            edit: { type: 'emit', id: i, href: '/company/driver-edit' }
          }
        });
      }
    }
  },
  methods: {
    openDriverView(id) {
      this.openedDriverView = !this.openedDriverView;
    },
    openDriverEdit(id) {
      this.openedDriverEdit = !this.openedDriverEdit;
    },
    onSubmitDriverEdit(e) {
      e.preventDefault();
      this.openedDriverEdit = !this.openedDriverEdit;
    },
    onSubmit(e) {
      var that = this;
      that.isValidated = true;
      
      var isValid = true;
      [
        'prefix', 'firstname', 'lastname', 'address', 'province', 'zipcode',
        'company', 'companyAddress', 'companyProvince', 'companyZipcode',
        'username', 'email', 'password', 'confPassword'
      ].forEach(function(k){
        if(!that.dataset[k]){
          isValid = false;
        }
      });

      if(!isValid){
        e.preventDefault();
      }else{
        that.isValidated = false;
      }
    }
  }
}
</script>
