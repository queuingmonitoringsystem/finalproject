<script>
    import { Navbar, NavBrand, NavLi, NavUl, NavHamburger, Avatar, Dropdown, DropdownItem, DropdownHeader, DropdownDivider } from 'flowbite-svelte';
  </script>
  
  <Navbar class="text-white" style="background: #1F4529">
    <NavBrand href="/">
      <!-- <img src="/images/flowbite-svelte-icon-logo.svg" class="me-3 h-6 sm:h-9" alt="Flowbite Logo" /> -->
      <span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">SwiftServe</span>
    </NavBrand>
    <!-- <div class="flex items-center md:order-2">
      <Avatar id="avatar-menu" src="assets/pictures/jenishe.jpg" />
    </div> -->
    <Dropdown placement="bottom" triggeredBy="#avatar-menu">
      <DropdownHeader>
        <span class="block text-sm">Jenishe Salem</span>
        <span class="block truncate text-sm font-medium">jenishedufsalem@gmail.com</span>
      </DropdownHeader>
      <DropdownItem href="https://coneofjen16.blogspot.com/">Blog</DropdownItem>
      <DropdownItem href="https://drive.google.com/drive/folders/117UTa4WLuXrMME9sNgpEOIrRA8WJbaMN?usp=drive_link">Video Presentation</DropdownItem>
      <DropdownItem href="https://github.com/jenishe-X">Github</DropdownItem>

    </Dropdown>
    <NavUl>
      <NavLi class="text-white" href="/">Home</NavLi>
      <NavLi class="text-white" href="/portfolio">Portfolio</NavLi>
      <NavLi class="text-white" href="/about">About</NavLi>
      <NavLi class="text-white" href="contact">Contact</NavLi>
    </NavUl>
  </Navbar>