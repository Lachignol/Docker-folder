NAME = Back2Home
CC = gcc
CFLAGS = -Wno-deprecated-declarations -g
LDFLAGS = /usr/lib/x86_64-linux-gnu/libcurl.a \
    -lssl -lcrypto -lgssapi_krb5 -lnghttp2 -lz -ldl -lm \
    /usr/lib/x86_64-linux-gnu/libldap.a \
    /usr/lib/x86_64-linux-gnu/liblber.a -lsasl2 -lssh -lpsl \
    -lzstd -lbrotlicommon -lbrotlidec -lrtmp -lidn2 \
    -lgnutls -lgcrypt -lgpg-error -lunistring -lnettle -lpthread
MAKEFLAGS += --no-print-directory

# Colors
GREEN = \033[0;32m
YELLOW = \033[0;33m
BLUE = \033[0;34m
MAGENTA = \033[0;35m
RESET = \033[0m

# Directories
SRC_DIR = src
OBJ_DIR = obj
INC_DIR = includes

# Include (.h)
INCLUDES = $(addprefix -I, $(INC_DIR))

# Sources
SRC = $(shell find $(SRC_DIR) -name "*.c")

# Objects
OBJ = $(SRC:%.c=$(OBJ_DIR)/%.o)

all: $(NAME)

$(OBJ_DIR)/%.o: %.c
	@mkdir -p $(OBJ_DIR)/$(dir $<)
	@echo "$(BLUE)Compiling:$(RESET) $<"
	@$(CC) $(CFLAGS) $(INCLUDES) -c $< -o $@


$(NAME): $(OBJ)
	@echo "$(YELLOW)Linking $(NAME)...$(RESET)"
	@$(CC) $(OBJ) -o $(NAME) $(LDFLAGS)
	@echo "$(GREEN)$(NAME) is ready!$(RESET)"

clean:
	@echo "$(YELLOW)Cleaning...$(RESET)"
	@rm -rf $(OBJ_DIR)
	@echo "$(GREEN)Clean complete!$(RESET)"

fclean:
	@echo "$(YELLOW)Full cleaning...$(RESET)"
	@echo "Cleaning exercice object files..."
	@rm -rf $(OBJ_DIR)
	@echo "Removing executable..."
	@rm -f $(NAME)
