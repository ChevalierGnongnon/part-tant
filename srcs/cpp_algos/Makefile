NAME = text_analyser

FILES = main

SRCS_DIR = srcs
OBJS_DIR = obj

SOURCES= $(foreach f, $(FILES), $(SRCS_DIR)/$(f).cpp)
OBJECTS= $(foreach f, $(FILES), $(OBJS_DIR)/$(f).o)
DEPS= $(OBJECTS:.o=.d)

TEST_INPUT = tests/phrases.txt

RM = rm -rf

CXX = c++

CXXFLAGS = -Werror -Wextra -Wall -std=c++20 -g -MMD -MP

VALGRIND = valgrind --leak-check=full --show-leak-kinds=all --track-origins=yes \
		   --errors-for-leak-kinds=definite,indirect --error-exitcode=1

all: $(NAME)

$(NAME): $(OBJECTS)
	$(CXX) $(CXXFLAGS) $(OBJECTS) -o $(NAME)

$(OBJS_DIR)/%.o: $(SRCS_DIR)/%.cpp
	@mkdir -p $(dir $@)
	$(CXX) $(CXXFLAGS) -c $< -o $@

clean:
	$(RM) $(OBJS_DIR)

fclean: clean
	$(RM) $(NAME)

re:
	$(MAKE) fclean
	$(MAKE) all

leak_check: all
	$(VALGRIND) ./$(NAME) < $(TEST_INPUT)

-include $(DEPS)

.PHONY: all clean fclean re leak_check
