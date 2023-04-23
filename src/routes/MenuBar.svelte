<script lang="ts">
    import Drawer, {
    Content,
    Header,
    Title,
    Subtitle,
  } from '@smui/drawer';
  import List, { Item, Text, Graphic } from '@smui/list';

  let sidebar: Drawer;
  let menubar_open = false;

  export function openMenu() {
    menubar_open = true;
    setTimeout(() => document.addEventListener("click", clickOutside), 1);  // small delay so it doesnt trigger from initial button click
  }

  function closeMenu() {
    menubar_open = false;
    document.removeEventListener("click", clickOutside);
  }

  const clickOutside = function(event: any) {
      var path = event.composedPath();

      if (!path.includes(sidebar.getElement())) {
        closeMenu();
      }
  }


</script>

<Drawer variant="modal" fixed={false} bind:open={menubar_open} bind:this={sidebar}>
  <Header>
    <Title>Pied Biker</Title>
    <Subtitle>Options</Subtitle>
  </Header>
  <Content>
        <List>
            <Item>
                <Text>Test</Text>
            </Item>
        </List>
  </Content>
</Drawer>
