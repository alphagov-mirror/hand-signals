<template>
  <div class="tray-button-outer" tabindex="0" @focus="closeDropdown" @keyup.enter="sendResponse()" @click="sendResponse()">
    <a class="tray-button" tabindex="-1" aria-label="Respond to a point" role="button">
      <div class="tray-button-bg"></div>
      <img :src="getResponse" style="height: 32px;" alt="I want to respond"/>
      <span class="tooltiptext">I want to respond</span>
    </a>
  </div>
</template>

<script>
import { generateUUID } from "../../../utils/index"

let RESPOND;
export default {
  const: RESPOND = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEsAAABLCAYAAAA4TnrqAAAACXBIWXMAAC4jAAAuIwF4pT92AAAJv2lUWHRYTUw6Y29tLmFkb2JlLnhtcAAAAAAAPD94cGFja2V0IGJlZ2luPSLvu78iIGlkPSJXNU0wTXBDZWhpSHpyZVN6TlRjemtjOWQiPz4gPHg6eG1wbWV0YSB4bWxuczp4PSJhZG9iZTpuczptZXRhLyIgeDp4bXB0az0iQWRvYmUgWE1QIENvcmUgNi4wLWMwMDIgNzkuMTY0MzUyLCAyMDIwLzAxLzMwLTE1OjUwOjM4ICAgICAgICAiPiA8cmRmOlJERiB4bWxuczpyZGY9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkvMDIvMjItcmRmLXN5bnRheC1ucyMiPiA8cmRmOkRlc2NyaXB0aW9uIHJkZjphYm91dD0iIiB4bWxuczp4bXA9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC8iIHhtbG5zOmRjPSJodHRwOi8vcHVybC5vcmcvZGMvZWxlbWVudHMvMS4xLyIgeG1sbnM6eG1wTU09Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9tbS8iIHhtbG5zOnN0RXZ0PSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvc1R5cGUvUmVzb3VyY2VFdmVudCMiIHhtbG5zOnN0UmVmPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvc1R5cGUvUmVzb3VyY2VSZWYjIiB4bWxuczpwaG90b3Nob3A9Imh0dHA6Ly9ucy5hZG9iZS5jb20vcGhvdG9zaG9wLzEuMC8iIHhtbG5zOnRpZmY9Imh0dHA6Ly9ucy5hZG9iZS5jb20vdGlmZi8xLjAvIiB4bWxuczpleGlmPSJodHRwOi8vbnMuYWRvYmUuY29tL2V4aWYvMS4wLyIgeG1wOkNyZWF0b3JUb29sPSJBZG9iZSBQaG90b3Nob3AgMjEuMSAoV2luZG93cykiIHhtcDpDcmVhdGVEYXRlPSIyMDIwLTA0LTI4VDE5OjUxOjE5KzAxOjAwIiB4bXA6TWV0YWRhdGFEYXRlPSIyMDIwLTA0LTI4VDIwOjAxOjE0KzAxOjAwIiB4bXA6TW9kaWZ5RGF0ZT0iMjAyMC0wNC0yOFQyMDowMToxNCswMTowMCIgZGM6Zm9ybWF0PSJpbWFnZS9wbmciIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6MmRjODJlZTktYWYxNC02NTQzLWIwMGEtNWZkOTAwYjBjODJkIiB4bXBNTTpEb2N1bWVudElEPSJhZG9iZTpkb2NpZDpwaG90b3Nob3A6MWI5NzJhMzItYWI3MC01MDQxLWE3NGQtNmM5ZWZmNTk4MTViIiB4bXBNTTpPcmlnaW5hbERvY3VtZW50SUQ9InhtcC5kaWQ6Y2IwN2Q0ZjQtNjlkNS00MjQ4LTgxYTAtMGIxYjJkODI3OTY3IiBwaG90b3Nob3A6Q29sb3JNb2RlPSIzIiBwaG90b3Nob3A6SUNDUHJvZmlsZT0ic1JHQiBJRUM2MTk2Ni0yLjEiIHRpZmY6T3JpZW50YXRpb249IjEiIHRpZmY6WFJlc29sdXRpb249IjMwMDAwMDAvMTAwMDAiIHRpZmY6WVJlc29sdXRpb249IjMwMDAwMDAvMTAwMDAiIHRpZmY6UmVzb2x1dGlvblVuaXQ9IjIiIGV4aWY6Q29sb3JTcGFjZT0iMSIgZXhpZjpQaXhlbFhEaW1lbnNpb249IjUyNyIgZXhpZjpQaXhlbFlEaW1lbnNpb249IjUyNiI+IDx4bXBNTTpIaXN0b3J5PiA8cmRmOlNlcT4gPHJkZjpsaSBzdEV2dDphY3Rpb249ImNyZWF0ZWQiIHN0RXZ0Omluc3RhbmNlSUQ9InhtcC5paWQ6Y2IwN2Q0ZjQtNjlkNS00MjQ4LTgxYTAtMGIxYjJkODI3OTY3IiBzdEV2dDp3aGVuPSIyMDIwLTA0LTI4VDE5OjUxOjE5KzAxOjAwIiBzdEV2dDpzb2Z0d2FyZUFnZW50PSJBZG9iZSBQaG90b3Nob3AgMjEuMSAoV2luZG93cykiLz4gPHJkZjpsaSBzdEV2dDphY3Rpb249InNhdmVkIiBzdEV2dDppbnN0YW5jZUlEPSJ4bXAuaWlkOjE3NTIzNjc0LWRiMTUtZGU0OS05YTliLTU5ZTBhNWM4NGIxZCIgc3RFdnQ6d2hlbj0iMjAyMC0wNC0yOFQyMDowMToxNCswMTowMCIgc3RFdnQ6c29mdHdhcmVBZ2VudD0iQWRvYmUgUGhvdG9zaG9wIDIxLjEgKFdpbmRvd3MpIiBzdEV2dDpjaGFuZ2VkPSIvIi8+IDxyZGY6bGkgc3RFdnQ6YWN0aW9uPSJjb252ZXJ0ZWQiIHN0RXZ0OnBhcmFtZXRlcnM9ImZyb20gYXBwbGljYXRpb24vdm5kLmFkb2JlLnBob3Rvc2hvcCB0byBpbWFnZS9wbmciLz4gPHJkZjpsaSBzdEV2dDphY3Rpb249ImRlcml2ZWQiIHN0RXZ0OnBhcmFtZXRlcnM9ImNvbnZlcnRlZCBmcm9tIGFwcGxpY2F0aW9uL3ZuZC5hZG9iZS5waG90b3Nob3AgdG8gaW1hZ2UvcG5nIi8+IDxyZGY6bGkgc3RFdnQ6YWN0aW9uPSJzYXZlZCIgc3RFdnQ6aW5zdGFuY2VJRD0ieG1wLmlpZDoyZGM4MmVlOS1hZjE0LTY1NDMtYjAwYS01ZmQ5MDBiMGM4MmQiIHN0RXZ0OndoZW49IjIwMjAtMDQtMjhUMjA6MDE6MTQrMDE6MDAiIHN0RXZ0OnNvZnR3YXJlQWdlbnQ9IkFkb2JlIFBob3Rvc2hvcCAyMS4xIChXaW5kb3dzKSIgc3RFdnQ6Y2hhbmdlZD0iLyIvPiA8L3JkZjpTZXE+IDwveG1wTU06SGlzdG9yeT4gPHhtcE1NOkRlcml2ZWRGcm9tIHN0UmVmOmluc3RhbmNlSUQ9InhtcC5paWQ6MTc1MjM2NzQtZGIxNS1kZTQ5LTlhOWItNTllMGE1Yzg0YjFkIiBzdFJlZjpkb2N1bWVudElEPSJ4bXAuZGlkOmNiMDdkNGY0LTY5ZDUtNDI0OC04MWEwLTBiMWIyZDgyNzk2NyIgc3RSZWY6b3JpZ2luYWxEb2N1bWVudElEPSJ4bXAuZGlkOmNiMDdkNGY0LTY5ZDUtNDI0OC04MWEwLTBiMWIyZDgyNzk2NyIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PlTnq1AAAAysSURBVHic7Zx5kFzFfcc//Y45dvbWLqsDySuhRSuBriJljIQEiSEoGMVgYwgkhpTBriKOics4cbADlTgJ4Q+IHQxOiIlTGHPEGAxlCwJIwpIxZUFQEBKWV5KRdnXtPcfunO/o/NGzu7OrPeZ4sxqJfKqmpvYdv/697/Tr7f71r1tc8MoJTgPN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",
  computed: {
    getResponse() {
      return RESPOND;
    },
    getUsername() {
      if (this.$store.state.isFullName) {
        return this.$store.getters.getUser("fullName");
      } else {
        return this.$store.getters.getUser("name");
      }
    }
  },
  methods: {
    sendResponse() {
      // Close dropdown
      this.$store.dispatch("closeDropdown", "reactions");
      //Generate id
      const id = generateUUID();
      // Send local version to store
      if (this.$store.state.response.filter(h => h.owner === true).length < 1) {
        this.$store.dispatch("addRespond", {
          emoji: "response",
          encoded: RESPOND,
          username: `${this.getUsername} wants to respond`,
          img: this.$store.getters.getUser("avatar"),
          messageId: id,
          owner: true
        });
        // Send one over the websocket to other users
        this.$socket.sendObj({
          action: "RESPONDQUEUE",
          message: {
            id: this.$store.getters.getUser("meetingID"),
            emoji: "response",
            encoded: RESPOND,
            username: `${this.getUsername} wants to respond`,
            img: this.$store.getters.getUser("avatar"),
            messageId: id
          }
        });
      }
    },
    closeDropdown() {
      this.$store.dispatch("closeDropdown", "reactions");
    }
  }
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
