<template>
  <div class="tray-button-outer" tabindex="0" @focus="closeDropdown" @click="sendMessage(emoji)" @keyup.enter="sendMessage(emoji)">
    <a class="tray-button" tabindex="-1" aria-label="I disagree" role="button">
      <div class="tray-button-bg"></div>
      <img :src="getDisagree" style="height: 32px;" alt="I disagree"/>
      <span class="tooltiptext">I disagree</span>
    </a>
  </div>
</template>

<script>
  import { generateUUID } from "../../../utils/index";

  let DISAGREE;
  export default {
  props: {
    encoded: String,
    text: String,
    label: String
  },

  const: DISAGREE ="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEsAAABLCAYAAAA4TnrqAAAACXBIWXMAAC4jAAAuIwF4pT92AAAJv2lUWHRYTUw6Y29tLmFkb2JlLnhtcAAAAAAAPD94cGFja2V0IGJlZ2luPSLvu78iIGlkPSJXNU0wTXBDZWhpSHpyZVN6TlRjemtjOWQiPz4gPHg6eG1wbWV0YSB4bWxuczp4PSJhZG9iZTpuczptZXRhLyIgeDp4bXB0az0iQWRvYmUgWE1QIENvcmUgNi4wLWMwMDIgNzkuMTY0MzUyLCAyMDIwLzAxLzMwLTE1OjUwOjM4ICAgICAgICAiPiA8cmRmOlJERiB4bWxuczpyZGY9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkvMDIvMjItcmRmLXN5bnRheC1ucyMiPiA8cmRmOkRlc2NyaXB0aW9uIHJkZjphYm91dD0iIiB4bWxuczp4bXA9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC8iIHhtbG5zOmRjPSJodHRwOi8vcHVybC5vcmcvZGMvZWxlbWVudHMvMS4xLyIgeG1sbnM6eG1wTU09Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9tbS8iIHhtbG5zOnN0RXZ0PSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvc1R5cGUvUmVzb3VyY2VFdmVudCMiIHhtbG5zOnN0UmVmPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvc1R5cGUvUmVzb3VyY2VSZWYjIiB4bWxuczpwaG90b3Nob3A9Imh0dHA6Ly9ucy5hZG9iZS5jb20vcGhvdG9zaG9wLzEuMC8iIHhtbG5zOnRpZmY9Imh0dHA6Ly9ucy5hZG9iZS5jb20vdGlmZi8xLjAvIiB4bWxuczpleGlmPSJodHRwOi8vbnMuYWRvYmUuY29tL2V4aWYvMS4wLyIgeG1wOkNyZWF0b3JUb29sPSJBZG9iZSBQaG90b3Nob3AgMjEuMSAoV2luZG93cykiIHhtcDpDcmVhdGVEYXRlPSIyMDIwLTA0LTI4VDE5OjUxOjU0KzAxOjAwIiB4bXA6TWV0YWRhdGFEYXRlPSIyMDIwLTA0LTI4VDIwOjAxOjM4KzAxOjAwIiB4bXA6TW9kaWZ5RGF0ZT0iMjAyMC0wNC0yOFQyMDowMTozOCswMTowMCIgZGM6Zm9ybWF0PSJpbWFnZS9wbmciIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6MDYyZGI3YzItMTI0Yy0xNzRiLWEzZGYtOWU2ODk0NjVhZmM4IiB4bXBNTTpEb2N1bWVudElEPSJhZG9iZTpkb2NpZDpwaG90b3Nob3A6YWQ1MGViM2UtYjE4Ni0wMDQ0LTg5ZTAtMzBiNzdjNWIyYWIzIiB4bXBNTTpPcmlnaW5hbERvY3VtZW50SUQ9InhtcC5kaWQ6Y2NmNzg5ZDMtZjM4Yi02NDQ2LWFiNWQtZjc1NGVjZDZmNTllIiBwaG90b3Nob3A6Q29sb3JNb2RlPSIzIiBwaG90b3Nob3A6SUNDUHJvZmlsZT0ic1JHQiBJRUM2MTk2Ni0yLjEiIHRpZmY6T3JpZW50YXRpb249IjEiIHRpZmY6WFJlc29sdXRpb249IjMwMDAwMDAvMTAwMDAiIHRpZmY6WVJlc29sdXRpb249IjMwMDAwMDAvMTAwMDAiIHRpZmY6UmVzb2x1dGlvblVuaXQ9IjIiIGV4aWY6Q29sb3JTcGFjZT0iMSIgZXhpZjpQaXhlbFhEaW1lbnNpb249IjUyNyIgZXhpZjpQaXhlbFlEaW1lbnNpb249IjUyNiI+IDx4bXBNTTpIaXN0b3J5PiA8cmRmOlNlcT4gPHJkZjpsaSBzdEV2dDphY3Rpb249ImNyZWF0ZWQiIHN0RXZ0Omluc3RhbmNlSUQ9InhtcC5paWQ6Y2NmNzg5ZDMtZjM4Yi02NDQ2LWFiNWQtZjc1NGVjZDZmNTllIiBzdEV2dDp3aGVuPSIyMDIwLTA0LTI4VDE5OjUxOjU0KzAxOjAwIiBzdEV2dDpzb2Z0d2FyZUFnZW50PSJBZG9iZSBQaG90b3Nob3AgMjEuMSAoV2luZG93cykiLz4gPHJkZjpsaSBzdEV2dDphY3Rpb249InNhdmVkIiBzdEV2dDppbnN0YW5jZUlEPSJ4bXAuaWlkOjY0NTQ0NWNiLWIyZjQtY2Y0My1hY2JkLWFhY2Y2ZmE0NWYwOCIgc3RFdnQ6d2hlbj0iMjAyMC0wNC0yOFQyMDowMTozOCswMTowMCIgc3RFdnQ6c29mdHdhcmVBZ2VudD0iQWRvYmUgUGhvdG9zaG9wIDIxLjEgKFdpbmRvd3MpIiBzdEV2dDpjaGFuZ2VkPSIvIi8+IDxyZGY6bGkgc3RFdnQ6YWN0aW9uPSJjb252ZXJ0ZWQiIHN0RXZ0OnBhcmFtZXRlcnM9ImZyb20gYXBwbGljYXRpb24vdm5kLmFkb2JlLnBob3Rvc2hvcCB0byBpbWFnZS9wbmciLz4gPHJkZjpsaSBzdEV2dDphY3Rpb249ImRlcml2ZWQiIHN0RXZ0OnBhcmFtZXRlcnM9ImNvbnZlcnRlZCBmcm9tIGFwcGxpY2F0aW9uL3ZuZC5hZG9iZS5waG90b3Nob3AgdG8gaW1hZ2UvcG5nIi8+IDxyZGY6bGkgc3RFdnQ6YWN0aW9uPSJzYXZlZCIgc3RFdnQ6aW5zdGFuY2VJRD0ieG1wLmlpZDowNjJkYjdjMi0xMjRjLTE3NGItYTNkZi05ZTY4OTQ2NWFmYzgiIHN0RXZ0OndoZW49IjIwMjAtMDQtMjhUMjA6MDE6MzgrMDE6MDAiIHN0RXZ0OnNvZnR3YXJlQWdlbnQ9IkFkb2JlIFBob3Rvc2hvcCAyMS4xIChXaW5kb3dzKSIgc3RFdnQ6Y2hhbmdlZD0iLyIvPiA8L3JkZjpTZXE+IDwveG1wTU06SGlzdG9yeT4gPHhtcE1NOkRlcml2ZWRGcm9tIHN0UmVmOmluc3RhbmNlSUQ9InhtcC5paWQ6NjQ1NDQ1Y2ItYjJmNC1jZjQzLWFjYmQtYWFjZjZmYTQ1ZjA4IiBzdFJlZjpkb2N1bWVudElEPSJ4bXAuZGlkOmNjZjc4OWQzLWYzOGItNjQ0Ni1hYjVkLWY3NTRlY2Q2ZjU5ZSIgc3RSZWY6b3JpZ2luYWxEb2N1bWVudElEPSJ4bXAuZGlkOmNjZjc4OWQzLWYzOGItNjQ0Ni1hYjVkLWY3NTRlY2Q2ZjU5ZSIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PjXpclcAABGvSURBVHic5Zx5lF1Fncc/d3n37a+X13tn6SUrTUhiILIEQiBIXAAZlBlH4Qhuw+hRRh2OjiMIx6NnxBnHFRxmQHFwMsAccQQ1TiLL6BhIRkKAFrMA6Q70lt6733bvrZo/qpd3+77upLtfkob5ntPLq1u36ve+91e/+tWvfnU1d+fVnAbUAsuB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",
  computed: {
    canPost() {
      return this.$store.state.messages.filter((h) => h.owner === true).length < 1;
    },
    getDisagree() {
          return DISAGREE;
    },
    getUsername() {
      if (this.$store.state.isFullName) {
        return this.$store.getters.getUser("fullName");
      } else {
        return this.$store.getters.getUser("name");
      }
    },
  },
  methods: {
    sendMessage(emoji) {
      this.$store.dispatch("closeDropdown", "reactions");
      if (this.canPost) {
        this.$store.dispatch("addMessage", {
          messageId: generateUUID(),
          encoded: DISAGREE,
          username: this.getUsername,
          img: this.$store.getters.getUser("avatar"),
          owner: true
        });

        this.$socket.sendObj({
          action: "MESSAGE",
          message: {
            id: this.$store.getters.getUser("meetingID"),
            encoded: DISAGREE,
            username: this.getUsername,
            img: this.$store.getters.getUser("avatar"),
          },
        });
      }
    },
  },
};
</script>

<style lang="scss" scoped>
  .tray-button-outer {
  &:focus > .tray-button {
     background-color: rgba(2, 191, 165, 0.15);
   }
  }

  .tray-button {
    display: flex;
    overflow: visible !important;
    padding: 0 10px;
  }
</style>
